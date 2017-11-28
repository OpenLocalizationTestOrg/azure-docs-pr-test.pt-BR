---
title: "Configurando a telemetria dos Serviços de Mídia do Azure com o .NET | Microsoft Docs"
description: "Este artigo mostra como usar a telemetria dos Serviços de Mídia do Azure usando o SDK do .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 1d857f3d062d8d1b15c64fa4b8c3e27ad6c2247e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="60cc0-103">Configurando a telemetria dos Serviços de Mídia do Azure com o .NET</span><span class="sxs-lookup"><span data-stu-id="60cc0-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="60cc0-104">Este tópico descreve as etapas gerais que podem ser seguidas ao configurar a telemetria de serviços de mídia do Azure (AMS) usando o SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="60cc0-104">This topic describes general steps that you might take when configuring the Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="60cc0-105">Para obter uma explicação detalhada do que é a telemetria do AMS e como consumi-la, consulte o tópico [visão geral](media-services-telemetry-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60cc0-105">For the detailed explanation of what is AMS telemetry and how to consume it, see the [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="60cc0-106">É possível consumir os dados de telemetria das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="60cc0-106">You can consume telemetry data in one of the following ways:</span></span>

- <span data-ttu-id="60cc0-107">Leia os dados diretamente no Armazenamento de Tabelas do Azure (por exemplo, usando o SDK de Armazenamento).</span><span class="sxs-lookup"><span data-stu-id="60cc0-107">Read data directly from Azure Table Storage (e.g. using the Storage SDK).</span></span> <span data-ttu-id="60cc0-108">Para obter a descrição das tabelas de armazenamento de telemetria, confira **Consumindo informações de telemetria**[neste](https://msdn.microsoft.com/library/mt742089.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="60cc0-108">For the description of telemetry storage tables, see the **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="60cc0-109">Ou</span><span class="sxs-lookup"><span data-stu-id="60cc0-109">Or</span></span>

- <span data-ttu-id="60cc0-110">Use o suporte do SDK para .NET dos Serviços de Mídia para leitura de dados de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="60cc0-110">Use the support in the Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="60cc0-111">Este tópico mostra como habilitar a telemetria para a conta AMS especificada e como consultar as métricas usando o SDK para .NET dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="60cc0-111">This topic shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="60cc0-112">Configurando a telemetria para uma conta dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="60cc0-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="60cc0-113">As etapas abaixo são necessárias para habilitar a telemetria:</span><span class="sxs-lookup"><span data-stu-id="60cc0-113">The following steps are needed to enable telemetry:</span></span>

- <span data-ttu-id="60cc0-114">Obter as credenciais da conta de armazenamento anexada à conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="60cc0-114">Get the credentials of the storage account attached to the Media Services account.</span></span> 
- <span data-ttu-id="60cc0-115">Criar um Ponto de Extremidade de Notificação com **EndPointType** definido como **AzureTable** e endPointAddress apontando para a tabela de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="60cc0-115">Create a Notification Endpoint with **EndPointType** set to **AzureTable** and endPointAddress pointing to the storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="60cc0-116">Criar definições de configuração de monitoramento para os serviços que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="60cc0-116">Create a monitoring configuration settings for the services you want to monitor.</span></span> <span data-ttu-id="60cc0-117">Não é permitida mais de uma definição de configuração de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="60cc0-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="60cc0-118">Consumindo informações de telemetria</span><span class="sxs-lookup"><span data-stu-id="60cc0-118">Consuming telemetry information</span></span>

<span data-ttu-id="60cc0-119">Para saber mais sobre o consumo de telemetria, consulte [este](media-services-telemetry-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="60cc0-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="60cc0-120">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="60cc0-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="60cc0-121">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="60cc0-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="60cc0-122">Adicione o seguinte elemento às **appSettings** definidas no seu arquivo app.config:</span><span class="sxs-lookup"><span data-stu-id="60cc0-122">Add the following element to **appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="60cc0-123">Exemplo</span><span class="sxs-lookup"><span data-stu-id="60cc0-123">Example</span></span>  
    
<span data-ttu-id="60cc0-124">O exemplo a seguir mostra habilitar a telemetria para a conta AMS especificada e como consultar as métricas usando o SDK para .NET dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="60cc0-124">The following example shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print the channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="60cc0-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60cc0-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="60cc0-126">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="60cc0-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
