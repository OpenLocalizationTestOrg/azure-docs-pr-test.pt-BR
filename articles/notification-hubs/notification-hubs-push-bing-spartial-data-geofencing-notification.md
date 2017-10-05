---
title: "Notificações por push com delimitação geográfica com os Hubs de Notificação do Azure e o Bing Spatial Data | Microsoft Docs"
description: "Neste tutorial, você aprenderá a entregar notificações por push baseadas na localização com os Hubs de Notificação do Azure e o Bing Spatial Data."
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
ms.openlocfilehash: b2a84e0479aac9ded08bb64e1ea20ddee6636cce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="75b17-104">Notificações por push com delimitação geográfica com os Hubs de Notificação do Azure e o Bing Spatial Data</span><span class="sxs-lookup"><span data-stu-id="75b17-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="75b17-105">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="75b17-105">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="75b17-106">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="75b17-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="75b17-107">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="75b17-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="75b17-108">Neste tutorial, você aprenderá a enviar notificações por push baseadas na localização com os Hubs de Notificação do Azure e o Bing Spatial Data em um aplicativo da Plataforma Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="75b17-108">In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75b17-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="75b17-109">Prerequisites</span></span>
<span data-ttu-id="75b17-110">Primeiro, você precisa se certificar de que tem todos os pré-requisitos de software e de serviço:</span><span class="sxs-lookup"><span data-stu-id="75b17-110">First and foremost, you need to make sure that you have all the software and service pre-requisites:</span></span>

* <span data-ttu-id="75b17-111">[Visual Studio 2015 Atualização 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) ou posterior (o [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) também servirá).</span><span class="sxs-lookup"><span data-stu-id="75b17-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="75b17-112">Versão mais recente do [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="75b17-112">Latest version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="75b17-113">[Conta do Centro de Desenvolvimento do Bing Mapas](https://www.bingmapsportal.com/) (você pode criá-la gratuitamente e associá-la à sua conta da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="75b17-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="75b17-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="75b17-114">Getting Started</span></span>
<span data-ttu-id="75b17-115">Vamos começar pela criação do projeto.</span><span class="sxs-lookup"><span data-stu-id="75b17-115">Let’s start by creating the project.</span></span> <span data-ttu-id="75b17-116">No Visual Studio, inicie um novo projeto do tipo **Aplicativo em Branco (Universal do Windows)**.</span><span class="sxs-lookup"><span data-stu-id="75b17-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="75b17-117">Uma vez concluída a criação do projeto, você deverá ter o agente para o próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75b17-117">Once the project creation is complete, you should have the harness for the app itself.</span></span> <span data-ttu-id="75b17-118">Agora vamos configurar tudo para a infraestrutura de delimitação geográfica.</span><span class="sxs-lookup"><span data-stu-id="75b17-118">Now let’s set up everything for the geo-fencing infrastructure.</span></span> <span data-ttu-id="75b17-119">Como vamos usar os serviços do Bing para isso, há um ponto de extremidade de API REST público que permite consultar quadros de local específico:</span><span class="sxs-lookup"><span data-stu-id="75b17-119">Because we are going to use Bing services for this, there is a public REST API endpoint that allows us to query specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="75b17-120">Você precisará especificar os parâmetros a seguir para fazer isso funcionar:</span><span class="sxs-lookup"><span data-stu-id="75b17-120">You will need to specify the following parameters to get it working:</span></span>

* <span data-ttu-id="75b17-121">**ID da Fonte de Dados** e **Nome da Fonte de Dados** – na API do Bing Mapas, as fontes de dados contêm diversos metadados classificados, como locais e horas comerciais de operação.</span><span class="sxs-lookup"><span data-stu-id="75b17-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="75b17-122">Leia mais sobre isso aqui.</span><span class="sxs-lookup"><span data-stu-id="75b17-122">You can read more about those here.</span></span> 
* <span data-ttu-id="75b17-123">**Nome da Entidade** – a entidade que você deseja usar como um ponto de referência para a notificação.</span><span class="sxs-lookup"><span data-stu-id="75b17-123">**Entity Name** – the entity you want to use as a reference point for the notification.</span></span> 
* <span data-ttu-id="75b17-124">**Chave de API do Bing Mapas** – é a chave que você obteve anteriormente quando criou a conta do Centro de Desenvolvimento do Bing.</span><span class="sxs-lookup"><span data-stu-id="75b17-124">**Bing Maps API Key** – this is the key that you obtained earlier when you created the Bing Dev Center account.</span></span>

<span data-ttu-id="75b17-125">Vamos fazer uma análise aprofundada sobre a instalação de cada um dos elementos acima.</span><span class="sxs-lookup"><span data-stu-id="75b17-125">Let’s do a deep-dive on the setup for each of the elements above.</span></span>

## <a name="setting-up-the-data-source"></a><span data-ttu-id="75b17-126">Configuração da fonte de dados</span><span class="sxs-lookup"><span data-stu-id="75b17-126">Setting up the data source</span></span>
<span data-ttu-id="75b17-127">Você pode fazer isso no Centro de Desenvolvimento do Bing Mapas.</span><span class="sxs-lookup"><span data-stu-id="75b17-127">You can do it in the Bing Maps Dev Center.</span></span> <span data-ttu-id="75b17-128">Basta clicar em **Fontes de dados** na barra de navegação superior e selecionar **Gerenciar Fontes de Dados**.</span><span class="sxs-lookup"><span data-stu-id="75b17-128">Simply click on **Data sources** in the top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="75b17-129">Se você não tiver trabalhado com a API do Bing Mapas antes, provavelmente não haverá fontes de dados presentes e, portanto, é possível criar uma nova clicando em Carregar dados em uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="75b17-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data to a data source.</span></span> <span data-ttu-id="75b17-130">Preencha todos os campos obrigatórios:</span><span class="sxs-lookup"><span data-stu-id="75b17-130">Make sure you fill out all the required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="75b17-131">Você deve estar imaginando – o que é o arquivo de dados e o que você deve carregar?</span><span class="sxs-lookup"><span data-stu-id="75b17-131">You might be wondering – what is the data file and what should you be uploading?</span></span> <span data-ttu-id="75b17-132">Para os fins deste teste, nós usaremos apenas a amostra baseada em pipe que enquadra uma área da orla marítima de São Francisco:</span><span class="sxs-lookup"><span data-stu-id="75b17-132">For the purposes of this test, we can just use the sample pipe-based that frames an area of the San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="75b17-133">O texto acima representa esta entidade:</span><span class="sxs-lookup"><span data-stu-id="75b17-133">The above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="75b17-134">Simplesmente copie e cole a cadeia de caracteres acima em um novo arquivo e salve-o como **NotificationHubsGeofence.pipe**; carregue-o no Centro de Desenvolvimento do Bing.</span><span class="sxs-lookup"><span data-stu-id="75b17-134">Simply copy and paste the string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in the Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="75b17-135">Poderá ser solicitada uma nova chave para a **Chave Mestra**, que é diferente da **Chave de Consulta**.</span><span class="sxs-lookup"><span data-stu-id="75b17-135">You might be prompted to specify a new key for the **Master Key** that is different from the **Query Key**.</span></span> <span data-ttu-id="75b17-136">Basta criar uma nova chave por meio do painel e atualizar a página de carregamento da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="75b17-136">Simply create a new key through the dashboard and refresh the data source upload page.</span></span>
> 
> 

<span data-ttu-id="75b17-137">Depois que você carregar o arquivo de dados, deverá publicar a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="75b17-137">Once you upload the data file, you will need to make sure that you publish the data source.</span></span> 

<span data-ttu-id="75b17-138">Vá para **Gerenciar Fontes de Dados**, exatamente como fizemos acima, localize a fonte de dados na lista e clique em **Publicar** na coluna **Ações**.</span><span class="sxs-lookup"><span data-stu-id="75b17-138">Go to **Manage Data Sources**, just like we did above, find your data source in the list and click on **Publish** in the **Actions** column.</span></span> <span data-ttu-id="75b17-139">Em instantes, você deverá ver sua fonte de dados na guia **Fontes de Dados Publicadas** :</span><span class="sxs-lookup"><span data-stu-id="75b17-139">In a bit, you should see your data source in the **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="75b17-140">Se você clicar em **Editar**, poderá ver rapidamente quais locais introduzimos nela:</span><span class="sxs-lookup"><span data-stu-id="75b17-140">If you click **Edit**, you will be able to see at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="75b17-141">Neste ponto, o portal não mostrará os limites geográficos que criamos. Tudo o que precisamos é uma confirmação de que o local especificado está na vizinhança certa.</span><span class="sxs-lookup"><span data-stu-id="75b17-141">At this point, the portal does not show you the boundaries for the geofence that we created – all we need is a confirmation that the location specified is in the right vicinity.</span></span>

<span data-ttu-id="75b17-142">Agora você tem todos os requisitos da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="75b17-142">Now you have all the requirements for the data source.</span></span> <span data-ttu-id="75b17-143">Para obter os detalhes na URL de solicitação para a chamada à API, no Centro de Desenvolvimento do Bing Mapas, clique em **Fontes de dados** e selecione **Informações da Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="75b17-143">To get the details on the request URL for the API call, in the Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="75b17-144">A **URL da Consulta** é o que queremos aqui.</span><span class="sxs-lookup"><span data-stu-id="75b17-144">The **Query URL** is what we’re after here.</span></span> <span data-ttu-id="75b17-145">Esse é o ponto de extremidade no qual podemos executar consultas para verificar se o dispositivo ainda está dentro dos limites de um local ou não.</span><span class="sxs-lookup"><span data-stu-id="75b17-145">This is the endpoint against which we can execute queries to check whether the device is currently within the boundaries of a location or not.</span></span> <span data-ttu-id="75b17-146">Para executar essa verificação, precisamos apenas executar uma chamada GET na URL de consulta, com os seguintes parâmetros anexados:</span><span class="sxs-lookup"><span data-stu-id="75b17-146">To perform this check, we simply need to execute a GET call against the query URL, with the following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="75b17-147">Dessa forma, você está especificando um ponto de destino obtido do dispositivo e o Bing Mapas executará automaticamente os cálculos para ver se ele está dentro do limite geográfico.</span><span class="sxs-lookup"><span data-stu-id="75b17-147">That way you're specifying a target point that we obtain from the device and Bing Maps will automatically perform the calculations to see whether it is within the geofence.</span></span> <span data-ttu-id="75b17-148">Depois de executar a solicitação por meio de um navegador (ou cURL), você obterá uma resposta JSON padrão:</span><span class="sxs-lookup"><span data-stu-id="75b17-148">Once you execute the request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="75b17-149">Essa resposta só acontece quando o ponto está realmente dentro dos limites designados.</span><span class="sxs-lookup"><span data-stu-id="75b17-149">This response only happens when the point is actually within the designated boundaries.</span></span> <span data-ttu-id="75b17-150">Caso contrário, você obterá um bucket vazio de **resultados** :</span><span class="sxs-lookup"><span data-stu-id="75b17-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-the-uwp-application"></a><span data-ttu-id="75b17-151">Configuração do aplicativo UWP</span><span class="sxs-lookup"><span data-stu-id="75b17-151">Setting up the UWP application</span></span>
<span data-ttu-id="75b17-152">Agora que a fonte de dados está pronta, podemos começar a trabalhar no aplicativo UWP que inicializamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="75b17-152">Now that we have the data source ready, we can start working on the UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="75b17-153">Primeiro, devemos habilitar os serviços de localização para o nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75b17-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="75b17-154">Para isso, clique duas vezes no arquivo `Package.appxmanifest` no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="75b17-154">To do this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="75b17-155">Na guia de propriedades do pacote que acabou de abrir, clique em **Recursos** e selecione **Local**:</span><span class="sxs-lookup"><span data-stu-id="75b17-155">In the package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="75b17-156">Como o recurso local é declarado, crie uma nova pasta na solução denominada `Core` e adicione um novo arquivo a ela, chamado `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="75b17-156">As the location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="75b17-157">A classe `LocationHelper` em si é bem básica neste ponto – tudo o que ela faz é permitir a obtenção da localização do usuário por meio da API do sistema:</span><span class="sxs-lookup"><span data-stu-id="75b17-157">The `LocationHelper` class itself is fairly basic at this point – all it does is allow us to obtain the user location through the system API:</span></span>

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

<span data-ttu-id="75b17-158">Você pode ler mais sobre como obter a localização do usuário em aplicativos UWP no [documento do MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx)oficial.</span><span class="sxs-lookup"><span data-stu-id="75b17-158">You can read more about getting the user’s location in UWP apps in the official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="75b17-159">Para verificar se a aquisição da localização está funcionando, abra o lado do código da página principal (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="75b17-159">To check that the location acquisition is actually working, open the code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="75b17-160">Criar um novo manipulador de eventos para o evento `Loaded` no construtor `MainPage`:</span><span class="sxs-lookup"><span data-stu-id="75b17-160">Create a new event handler for the `Loaded` event in the `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="75b17-161">A implementação do manipulador de eventos é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="75b17-161">The implementation of the event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="75b17-162">Observe que declaramos o manipulador como assíncrono porque `GetCurrentLocation` é aguardável e, portanto, exige ser executado em um contexto assíncrono.</span><span class="sxs-lookup"><span data-stu-id="75b17-162">Notice that we declared the handler as async because `GetCurrentLocation` is awaitable, and therefore requires to be executed in an async context.</span></span> <span data-ttu-id="75b17-163">Além disso, como sob determinadas circunstâncias podemos terminar com uma localização nula (por exemplo, os serviços de localização estão desabilitados ou o aplicativo não teve permissões para acessar a localização), precisamos garantir que ele seja adequadamente manipulado com uma verificação de nulo.</span><span class="sxs-lookup"><span data-stu-id="75b17-163">Also, because under certain circumstances we might end up with a null location (e.g. the location services are disabled or the application was denied permissions to access location), we need to make sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="75b17-164">Execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75b17-164">Run the application.</span></span> <span data-ttu-id="75b17-165">Permita o acesso de localização:</span><span class="sxs-lookup"><span data-stu-id="75b17-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="75b17-166">Assim que o aplicativo for iniciado, você deverá ser capaz de ver as coordenadas na janela **Saída** :</span><span class="sxs-lookup"><span data-stu-id="75b17-166">Once the application launches, you should be able to see the coordinates in the **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="75b17-167">Agora você sabe que a aquisição de localização funciona – fique à vontade para remover o manipulador de eventos de teste carregado porque nós não o utilizarem mais.</span><span class="sxs-lookup"><span data-stu-id="75b17-167">Now you know that location acquisition works – feel free to remove the test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="75b17-168">A próxima etapa é capturar as alterações de localização.</span><span class="sxs-lookup"><span data-stu-id="75b17-168">The next step is to capture location changes.</span></span> <span data-ttu-id="75b17-169">Para isso, vamos voltar para a classe `LocationHelper` e adicionar o manipulador de eventos para `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="75b17-169">For that, let’s go back to the `LocationHelper` class and add the event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="75b17-170">A implementação mostrará as coordenadas de localização na janela **Saída** :</span><span class="sxs-lookup"><span data-stu-id="75b17-170">The implementation will show the location coordinates in the **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-the-backend"></a><span data-ttu-id="75b17-171">Configuração do back-end</span><span class="sxs-lookup"><span data-stu-id="75b17-171">Setting up the backend</span></span>
<span data-ttu-id="75b17-172">Baixe o [exemplo de back-end .NET do GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="75b17-172">Download the [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="75b17-173">Quando o download for concluído, abra a pasta `NotifyUsers` e depois o arquivo `NotifyUsers.sln`.</span><span class="sxs-lookup"><span data-stu-id="75b17-173">Once the download completes, open the `NotifyUsers` folder, and subsequently – the `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="75b17-174">Defina o projeto `AppBackend` como o **Projeto de Inicialização** e inicie-o.</span><span class="sxs-lookup"><span data-stu-id="75b17-174">Set the `AppBackend` project as the **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="75b17-175">O projeto já está configurado para enviar notificações por push para dispositivos de destino e, portanto, precisamos fazer somente duas coisas – trocar a cadeia de conexão correta para o hub de notificação e adicionar identificação de limite para enviar a notificação somente quando o usuário estiver dentro do limite geográfico.</span><span class="sxs-lookup"><span data-stu-id="75b17-175">The project is already configured to send push notifications to target devices, so we’ll need to do only two things – swap out the right connection string for the notification hub and add boundary identification to send the notification only when the user is within the geofence.</span></span>

<span data-ttu-id="75b17-176">Para configurar a cadeia de conexão, abra `Notifications.cs` na pasta `Models`.</span><span class="sxs-lookup"><span data-stu-id="75b17-176">To configure the connection string, in the `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="75b17-177">A função `NotificationHubClient.CreateClientFromConnectionString` deve conter as informações sobre o hub de notificação que você pode obter no [Portal do Azure](https://portal.azure.com) (examine a folha **Políticas de Acesso** em **Configurações**).</span><span class="sxs-lookup"><span data-stu-id="75b17-177">The `NotificationHubClient.CreateClientFromConnectionString` function should contain the information about your notification hub that you can get in the [Azure Portal](https://portal.azure.com) (look inside the **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="75b17-178">Salve o arquivo de configuração atualizado.</span><span class="sxs-lookup"><span data-stu-id="75b17-178">Save the updated configuration file.</span></span>

<span data-ttu-id="75b17-179">Agora precisamos criar um modelo para o resultado da API do Bing Mapas.</span><span class="sxs-lookup"><span data-stu-id="75b17-179">Now we need to create a model for the Bing Maps API result.</span></span> <span data-ttu-id="75b17-180">A maneira mais fácil de fazer isso é clicar com o botão direito do mouse na pasta `Models`, **Adicionar** > **Classe**.</span><span class="sxs-lookup"><span data-stu-id="75b17-180">The easiest way to do that is right-click on the `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="75b17-181">Nomeie-o `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="75b17-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="75b17-182">Quando tiver terminado, copie o JSON da resposta da API que abordamos na primeira seção e, no Visual Studio, use **Editar** > **Colar Especial** > **Colar JSON como Classes**.</span><span class="sxs-lookup"><span data-stu-id="75b17-182">Once done, copy the JSON from the API response that we discussed in the first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="75b17-183">Dessa forma, garantimos que o objeto será desserializado exatamente como foi pretendido.</span><span class="sxs-lookup"><span data-stu-id="75b17-183">That way we ensure that the object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="75b17-184">O conjunto de classes resultante deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="75b17-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="75b17-185">Em seguida, abra `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="75b17-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="75b17-186">É necessário ajustar a chamada Post para levar em consideração a latitude e a longitude do destino.</span><span class="sxs-lookup"><span data-stu-id="75b17-186">We need to tweak the Post call to account for the target longitude and latitude.</span></span> <span data-ttu-id="75b17-187">Para isso, basta adicionar duas cadeias de caracteres à assinatura da função – `latitude` e `longitude`.</span><span class="sxs-lookup"><span data-stu-id="75b17-187">For that, simply add two strings to the function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="75b17-188">Crie uma nova classe no projeto chamado `ApiHelper.cs` – nós a usaremos para a conexão com o Bing para criarmos pontos de verificação em interseções de limite.</span><span class="sxs-lookup"><span data-stu-id="75b17-188">Create a new class within the project called `ApiHelper.cs` – we’ll use it to connect to Bing to check point boundary intersections.</span></span> <span data-ttu-id="75b17-189">Implemente uma função `IsPointWithinBounds` , desta forma:</span><span class="sxs-lookup"><span data-stu-id="75b17-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="75b17-190">Substitua o ponto de extremidade de API pela URL de consulta obtida anteriormente do Centro de Desenvolvimento do Bing (o mesmo se aplica à chave de API).</span><span class="sxs-lookup"><span data-stu-id="75b17-190">Make sure to substitute the API endpoint with the query URL that you obtained earlier from the Bing Dev Center (same applies to the API key).</span></span> 
> 
> 

<span data-ttu-id="75b17-191">Se houver resultados para a consulta, isso significa que o ponto especificado está nos limites da delimitação geográfica e, portanto, retornamos `true`.</span><span class="sxs-lookup"><span data-stu-id="75b17-191">If there are results to the query, that means that the specified point is within the boundaries of the geofence, so we return `true`.</span></span> <span data-ttu-id="75b17-192">Se não houver nenhum resultado, o Bing está dizendo que o ponto está fora do quadro de pesquisa e, portanto, retornamos `false`.</span><span class="sxs-lookup"><span data-stu-id="75b17-192">If there are no results, Bing is telling us that the point is outside the lookup frame, so we return `false`.</span></span>

<span data-ttu-id="75b17-193">Novamente em `NotificationsController.cs`, crie uma verificação logo antes da instrução switch:</span><span class="sxs-lookup"><span data-stu-id="75b17-193">Back in `NotificationsController.cs`, create a check right before the switch statement:</span></span>

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

<span data-ttu-id="75b17-194">Dessa forma, a notificação só será enviada quando o ponto estiver dentro dos limites.</span><span class="sxs-lookup"><span data-stu-id="75b17-194">That way, the notification is only sent when the point is within the boundaries.</span></span>

## <a name="testing-push-notifications-in-the-uwp-app"></a><span data-ttu-id="75b17-195">Teste de notificações por push no aplicativo UWP</span><span class="sxs-lookup"><span data-stu-id="75b17-195">Testing push notifications in the UWP app</span></span>
<span data-ttu-id="75b17-196">Voltando ao aplicativo UWP, agora devemos conseguir testar as notificações.</span><span class="sxs-lookup"><span data-stu-id="75b17-196">Going back to the UWP app, we should now be able to test notifications.</span></span> <span data-ttu-id="75b17-197">Na classe `LocationHelper`, crie uma nova função – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="75b17-197">Within the `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="75b17-198">Troque o `POST_URL` para a localização do aplicativo Web implantado que criamos na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="75b17-198">Swap the `POST_URL` to the location of your deployed web application that we created in the previous section.</span></span> <span data-ttu-id="75b17-199">Por enquanto, é possível executá-lo localmente, mas à medida que você trabalhar na implantação de uma versão pública, precisará hospedá-lo em um provedor externo.</span><span class="sxs-lookup"><span data-stu-id="75b17-199">For now, it’s OK to run it locally, but as you work on deploying a public version, you will need to host it with an external provider.</span></span>
> 
> 

<span data-ttu-id="75b17-200">Agora vamos registrar o aplicativo UWP para notificações por push.</span><span class="sxs-lookup"><span data-stu-id="75b17-200">Let’s now make sure that we register the UWP app for push notifications.</span></span> <span data-ttu-id="75b17-201">No Visual Studio, clique em **Projeto** > **Loja** > **Associar aplicativo à loja**.</span><span class="sxs-lookup"><span data-stu-id="75b17-201">In Visual Studio, click on **Project** > **Store** > **Associate app with the store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="75b17-202">Depois que você entrar em sua conta de desenvolvedor, selecione um aplicativo existente ou crie um novo e associe o pacote a ele.</span><span class="sxs-lookup"><span data-stu-id="75b17-202">Once you sign in to your developer account, make sure you select an existing app or create a new one and associate the package with it.</span></span> 

<span data-ttu-id="75b17-203">Vá para o Centro de Desenvolvimento e abra o aplicativo que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="75b17-203">Go to the Dev Center and open the app that you just created.</span></span> <span data-ttu-id="75b17-204">Clique em **Serviços** > **Notificações por Push** > **Site dos Live Services**.</span><span class="sxs-lookup"><span data-stu-id="75b17-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="75b17-205">No site, anote o **Segredo do Aplicativo** e o **SID do Pacote**.</span><span class="sxs-lookup"><span data-stu-id="75b17-205">On the site, take note of the **Application Secret** and the **Package SID**.</span></span> <span data-ttu-id="75b17-206">Você precisará deles no Portal do Azure – abra seu hub de notificação, clique em **Configurações** > **Serviços de Notificação** > **Windows (WNS)** e insira as informações nos campos obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="75b17-206">You will need both in the Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter the information in the required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="75b17-207">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="75b17-207">Click on **Save**.</span></span>

<span data-ttu-id="75b17-208">Clique com o botão direito do mouse em **Referências** no **Gerenciador de Soluções** e selecione **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="75b17-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="75b17-209">Precisaremos adicionar uma referência à **biblioteca gerenciada do Barramento de Serviço do Microsoft Azure** – basta procurar `WindowsAzure.Messaging.Managed` e adicioná-lo ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="75b17-209">We will need to add a reference to the **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it to your project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="75b17-210">Para fins de teste, podemos criar o manipulador de eventos `MainPage_Loaded` novamente e adicionar este trecho de código a ele:</span><span class="sxs-lookup"><span data-stu-id="75b17-210">For testing purposes, we can create the `MainPage_Loaded` event handler once again, and add this code snippet to it:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays the registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="75b17-211">O trecho acima registra o aplicativo no hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="75b17-211">The above registers the app with the notification hub.</span></span> <span data-ttu-id="75b17-212">Você está pronto!</span><span class="sxs-lookup"><span data-stu-id="75b17-212">You are ready to go!</span></span> 

<span data-ttu-id="75b17-213">Em `LocationHelper`, no manipulador `Geolocator_PositionChanged`, você pode adicionar uma parte do código de teste que irá impor a colocação da localização dentro do limite geográfico:</span><span class="sxs-lookup"><span data-stu-id="75b17-213">In `LocationHelper`, inside the `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put the location inside the geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="75b17-214">Como não estamos passando as coordenadas reais (que podem não estar nos limites no momento) e como estamos usando valores predefinidos de teste, veremos uma notificação sobre atualização:</span><span class="sxs-lookup"><span data-stu-id="75b17-214">Because we are not passing the real coordinates (which might not be within the boundaries at the moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="75b17-215">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="75b17-215">What’s next?</span></span>
<span data-ttu-id="75b17-216">Existem algumas etapas que talvez você precise seguir além das anteriores para garantir que a solução esteja pronta para produção.</span><span class="sxs-lookup"><span data-stu-id="75b17-216">There are a couple of steps that you might need to follow in addition to the above to make sure that the solution is production-ready.</span></span>

<span data-ttu-id="75b17-217">Primeiro, talvez seja necessário garantir que os limites geográficos sejam dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="75b17-217">First and foremost, you might need to ensure that geofences are dynamic.</span></span> <span data-ttu-id="75b17-218">Isso exigirá algum trabalho extra com a API do Bing para poder carregar novos limites na fonte de dados existente.</span><span class="sxs-lookup"><span data-stu-id="75b17-218">This will require some extra work with the Bing API in order to be able to upload new boundaries within the existing data source.</span></span> <span data-ttu-id="75b17-219">Consulte a [documentação da API do Bing Spatial Data Services](https://msdn.microsoft.com/library/ff701734.aspx) para obter mais detalhes sobre o assunto.</span><span class="sxs-lookup"><span data-stu-id="75b17-219">Consult the [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on the subject.</span></span>

<span data-ttu-id="75b17-220">Segundo, como você está trabalhando para garantir que a entrega seja feita aos participantes certos, talvez você queira usar a [marcação](notification-hubs-tags-segment-push-message.md)para tê-los como destino.</span><span class="sxs-lookup"><span data-stu-id="75b17-220">Second, as you are working to ensure that the delivery is done to the right participants, you might want to target them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="75b17-221">A solução mostrada acima descreve um cenário em que você pode ter uma ampla variedade de plataformas de destino e, portanto, não limitamos a delimitação geográfica a recursos específicos do sistema.</span><span class="sxs-lookup"><span data-stu-id="75b17-221">The solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit the geofencing to system-specific capabilities.</span></span> <span data-ttu-id="75b17-222">Dito isso, a Plataforma Universal do Windows oferece recursos para [detectar delimitações geográficas prontas](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="75b17-222">That said, the Universal Windows Platform offers capabilities to [detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="75b17-223">Para obter mais detalhes sobre os recursos de Hubs de Notificação, confira nosso [portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="75b17-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

