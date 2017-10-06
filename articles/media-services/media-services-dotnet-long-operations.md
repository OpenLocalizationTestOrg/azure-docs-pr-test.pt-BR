---
title: "Operações de execução longa de aaaPolling | Microsoft Docs"
description: "Este tópico mostra como toopoll operações de execução longa."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a>Fornecendo mídia sob demanda com os Serviços de Mídia do Azure

## <a name="overview"></a>Visão geral

Serviços de mídia do Microsoft Azure oferece APIs que enviam solicitações de operações de toostart tooMedia serviços (por exemplo: criar, iniciar, interromper ou excluir um canal). Essas operações são de execução longa.

Olá Media Services .NET SDK fornece APIs que enviar solicitação hello e aguarde Olá toocomplete de operação (internamente, Olá APIs estão sondando o andamento da operação em alguns intervalos). Por exemplo, quando você chama o canal. Start (), o método hello retorna depois do início do canal de saudação. Você também pode usar a versão assíncrona Olá: await canal. StartAsync() (para obter informações sobre o padrão assíncrono baseado em tarefa, consulte [toque](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). APIs que enviam uma solicitação de operação e então sondam status Olá até Olá operação ser concluída são chamadas de "métodos de sondagem". Esses métodos (especialmente versão assíncrona Olá) são recomendados para aplicativos cliente avançados e/ou serviços com monitoração de estado.

Há cenários em que um aplicativo não puder aguardar uma solicitação http em tempo de execução e deseja toopoll de andamento da operação Olá manualmente. Um exemplo típico seria um navegador interagindo com um serviço web sem monitoração de estado: quando o navegador Olá solicitações toocreate um canal, serviço web de saudação inicia uma operação de longa duração e retorna Olá navegador de toohello de ID de operação. navegador de saudação pode então solicitar Olá web serviço tooget Olá status da operação com base na ID de saudação. Olá Media Services .NET SDK fornece APIs que são úteis para esse cenário. Essas APIs são chamadas de "métodos sem sondagem".
Olá, "métodos sem sondagem" têm saudação padrão de nomenclatura a seguir: enviar*OperationName*operação (por exemplo, SendCreateOperation). Enviar*OperationName*métodos de operação retornam Olá **IOperation** objeto; hello, objeto retornado contém informações que podem ser usados tootrack Olá operação. Olá enviar*OperationName*OperationAsync métodos retornam **tarefa<IOperation>**.

Atualmente, Olá métodos sem sondagem de classes de suporte a seguir: **Channel**, **StreamingEndpoint**, e **programa**.

toopoll para o status da operação hello, use Olá **GetOperation** método hello **OperationBaseCollection** classe. Use Olá status da operação de saudação toocheck intervalos a seguir: para **Channel** e **StreamingEndpoint** operações, use 30 segundos; para **programa** operações, use 10 segundos.

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Exemplo

Olá, exemplo a seguir define uma classe chamada **ChannelOperations**. Essa definição de classe pode ser um ponto de partida para a definição de classe de serviço Web. Para simplificar, hello exemplos a seguir usam versões assíncronas não Olá métodos.

exemplo Hello também mostra como o cliente Olá pode usar essa classe.

### <a name="channeloperations-class-definition"></a>Definição da classe ChannelOperations

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a>código de saudação do cliente
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

