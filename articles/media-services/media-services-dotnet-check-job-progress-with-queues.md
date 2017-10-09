---
title: "aaaUse fila do Azure storage toomonitor serviços de mídia notificações de trabalho com o .NET | Microsoft Docs"
description: "Saiba como toomonitor de armazenamento toouse fila do Azure Media Services trabalho notificações. exemplo de código Hello é escrito em c# e usa Olá SDK do Media Services para .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a>Usar notificações de trabalho de serviços de mídia do Azure fila armazenamento toomonitor com .NET
Quando você executar trabalhos de codificação, você geralmente requerem uma maneira tootrack trabalho de andamento. Você pode configurar as notificações do Media Services toodeliver muito[armazenamento de fila do Azure](../storage/storage-dotnet-how-to-use-queues.md). Você pode monitorar o andamento do trabalho, obtendo notificações de saudação armazenamento de fila. 

Mensagens entregues tooQueue armazenamento podem ser acessadas de qualquer lugar Olá, mundo. arquitetura de armazenamento de fila mensagens de saudação é altamente escalonável e confiável. É recomendável sondar o armazenamento de Filas em busca de mensagens, em vez de usar outros métodos.

Um cenário comum para notificações de serviços de escuta tooMedia é se você estiver desenvolvendo um sistema de gerenciamento de conteúdo que precisa tooperform algumas tarefas adicionais depois de um trabalho de codificação é concluída (por exemplo, tootrigger Olá próxima etapa em um fluxo de trabalho ou toopublish conteúdo).

Este tópico mostra como as mensagens de notificação tooget do armazenamento de fila.  

## <a name="considerations"></a>Considerações
Considere o seguinte Olá ao desenvolver aplicativos de serviços de mídia que usam o armazenamento de fila:

* O Armazenamento de filas não fornece uma garantia de entrega ordenada PEPS (primeiro a entrar, primeiro a sair). Para obter mais informações, consulte [Filas do Azure e Filas do Barramento de Serviço do Azure comparadas e contrastadas](https://msdn.microsoft.com/library/azure/hh767287.aspx).
* O Armazenamento de filas não é um serviço de envio por push. Você tem a fila de saudação toopoll.
* Você pode ter qualquer número de filas. Para obter mais informações, consulte [API REST do Serviço de Fila](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).
* Armazenamento de fila tem algumas limitações e especificações toobe atento. Elas são descritas em [Filas do Azure e Filas do Barramento de Serviço do Azure – semelhanças e diferenças](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).

## <a name="net-code-example"></a>Exemplo de código do .NET

exemplo de código Hello nesta seção Olá a seguir:

1. Define Olá **EncodingJobMessage** classe que mapeia toohello formato de mensagem de notificação. código de saudação desserializa mensagens recebidas da fila de saudação em objetos de saudação **EncodingJobMessage** tipo.
2. Carrega Olá serviços de mídia e informações de conta de armazenamento do arquivo App. config de saudação. exemplo de código de saudação usa essa saudação de toocreate informações **CloudMediaContext** e **CloudQueue** objetos.
3. Cria Olá fila que recebe mensagens de notificação sobre Olá trabalho de codificação.
4. Cria um ponto de extremidade que é mapeado toohello fila de notificação de saudação.
5. Anexa o trabalho de toohello de ponto de extremidade de notificação hello e envia o trabalho de codificação de saudação. Você pode ter vários notificação pontos de extremidade anexados tooa trabalho.
6. Passa **NotificationJobState.FinalStatesOnly** toohello **AddNew** método. (Neste exemplo, estamos interessados apenas nos Estados finais do processamento de um trabalho hello.)

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. Se você passar **NotificationJobState.All**, você obtém todos os Olá notificações de alteração de estado a seguir: enfileirado, agendado, processamento e concluído. No entanto, conforme observado anteriormente, o Armazenamento de filas não garante a entrega ordenada. tooorder mensagens, use Olá **Timestamp** propriedade (definidos no hello **EncodingJobMessage** tipo no exemplo hello abaixo). Há a possibilidade de mensagens duplicadas. toocheck duplicatas, use Olá **propriedade ETag** (definidos no hello **EncodingJobMessage** tipo). Também é possível que algumas notificações de alteração de estado sejam ignoradas.
8. Aguarda Olá trabalho tooget toohello concluída estado verificando saudação a cada 10 segundos. Exclui as mensagens depois que elas são processadas.
9. Exclui a fila de saudação e o ponto de extremidade de notificação de saudação.

> [!NOTE]
> Olá toomonitor de maneira recomendada que é de estado do trabalho por mensagens toonotification escuta, conforme mostrado no exemplo a seguir de saudação.
>
> Como alternativa, você pode verificar estado do trabalho usando Olá **IJob.State** propriedade.  Uma mensagem de notificação sobre a conclusão do trabalho poderá chegar antes do estado de saudação em **IJob** está definido muito**concluído**. Olá **IJob.State** propriedade reflete o estado de precisão de saudação com um pequeno atraso.
>
>

### <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

1. Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 
2. Crie uma nova pasta (pasta pode estar em qualquer lugar no disco local) e copie um arquivo. mp4 que você deseja tooencode e fluxo ou download progressivo. Neste exemplo, o caminho de "C:\Media" hello é usado.

### <a name="code"></a>Código

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want tooget messages from hello queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display hello message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete hello message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
Olá Olá anterior de exemplo produzido saída a seguir. Os valores variarão.

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a>Próxima etapa
Revise os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
