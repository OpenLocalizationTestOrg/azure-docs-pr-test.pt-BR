---
title: mensagens de aaaCloud para o dispositivo com o Azure IoT Hub (.NET) | Microsoft Docs
description: "Como toosend de nuvem para dispositivo mensagens tooa dispositivo de um hub IoT do Azure usando Olá SDKs de IoT do Azure para .NET. Modificar as mensagens de nuvem para dispositivo um dispositivo aplicativo tooreceive e modificar as mensagens de nuvem para dispositivo um aplicativo de back-end toosend hello."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>Enviar mensagens de dispositivo de tooyour Olá nuvem com o Hub IoT (.NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introdução
O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução. Olá [começar com o IoT Hub] tutorial mostra como toocreate um hub IoT, provisionar uma identidade de dispositivo nele e código de um aplicativo de dispositivo que envia mensagens de dispositivo para a nuvem.

Esse tutorial se baseia na [começar com o IoT Hub]. Ele mostra como:

* Sua solução back-end, envie mensagens de nuvem para dispositivo tooa único dispositivo por meio de IoT Hub.
* Receber mensagens da nuvem para o dispositivo em um dispositivo.
* De sua solução back-end, solicitar confirmação de entrega (*comentários*) para mensagens enviadas tooa dispositivo do IoT Hub.

Você pode encontrar mais informações sobre mensagens de nuvem para dispositivo em Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].

No final da saudação deste tutorial, você deve executar dois aplicativos de console do .NET:

* **SimulatedDevice**, uma versão modificada do aplicativo hello criado no [começar com o IoT Hub], que se conecta tooyour IoT hub e recebe mensagens de nuvem para dispositivo.
* **SendCloudToDevice**, que envia um aplicativo de dispositivo de toohello de mensagem de nuvem para dispositivo por meio de IoT Hub e, em seguida, recebe a sua confirmação de entrega.

> [!NOTE]
> O Hub IoT tem suporte a SDK para várias plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) nos [SDKs do dispositivo IoT do Azure]. Para obter instruções passo a passo sobre como tooconnect do seu dispositivo toothis tutorial código e geralmente tooAzure IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].
> 
> 

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

## <a name="receive-messages-in-hello-device-app"></a>Receber mensagens no aplicativo de dispositivo Olá
Nesta seção, você modificará o aplicativo para dispositivo Olá criado na [começar com o IoT Hub] tooreceive mensagens de nuvem para dispositivo do hub IoT de saudação.

1. No Visual Studio, no hello **SimulatedDevice** de projeto, adicione Olá após o método toohello **programa** classe.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    Olá `ReceiveAsync` método retorna de maneira assíncrona mensagem recebida em tempo de saudação são recebidos pelo dispositivo de saudação. Ele retorna *nulo* após um período de tempo limite especificáveis (nesse caso, padrão de saudação de um minuto é usado). Quando o aplicativo hello recebe um *nulo*, deveria continuar toowait novas mensagens. Esse requisito é motivo Olá Olá `if (receivedMessage == null) continue` linha.
   
    Olá chamada muito`CompleteAsync()` notifica o IoT Hub essa mensagem de saudação foi processada com êxito. mensagem de saudação com segurança pode ser removida da fila de dispositivo de saudação. Se algo acontecer esse aplicativo de dispositivo Olá impedido de concluir o processamento de mensagem de saudação hello, IoT Hub entrega novamente. Em seguida, é importante que lógica Olá dispositivo aplicativo de processamento de mensagens for *idempotente*, de modo que receber Olá mesma mensagem várias vezes produz Olá mesmo resultado. Um aplicativo pode também temporariamente abandonar uma mensagem, o que resulta em um hub IoT mantém a mensagem de saudação na fila de saudação para consumo futuro. Ou, o aplicativo hello pode rejeitar uma mensagem, que remove permanentemente a mensagem de saudação da fila de saudação. Para obter mais informações sobre o ciclo de vida de mensagem de nuvem para dispositivo Olá, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > Ao usar HTTP em vez de MQTT ou AMQP como transporte, Olá `ReceiveAsync` método retorna imediatamente. padrão de saudação com suporte para mensagens de nuvem para dispositivo com HTTP é dispositivos conectados intermitentemente que verifiquem mensagens raramente (menor cada 25 minutos). Emitir HTTP mais recebe os resultados em solicitações de saudação de limitação de IoT Hub. Para obter mais informações sobre as diferenças de saudação entre suporte MQTT, AMQP e HTTP e a limitação de Hub IoT, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].
   > 
   > 
2. Adicionar Olá seguinte método em Olá **principal** método antes de saudação `Console.ReadLine()` linha:
   
        ReceiveC2dAsync();

> [!NOTE]
> Para simplificar, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Envie uma mensagem da nuvem para o dispositivo
Nesta seção, você pode escrever um aplicativo de console .NET que envia mensagens de nuvem para dispositivo toohello dispositivo aplicativo.

1. Na solução atual do Visual Studio hello, criar um projeto de aplicativo de área de trabalho do Visual C# usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **SendCloudToDevice**.
   
    ![Novo projeto no Visual Studio][20]
2. No Gerenciador de soluções, clique com botão direito solução hello e, em seguida, clique em **gerenciar pacotes NuGet para solução...** . 
   
    Essa ação abre Olá **gerenciar pacotes NuGet** janela.
3. Procurar **Microsoft.Azure.Devices**, clique em **instalar**e aceite os termos de uso do hello. 
   
    Isso baixa, instala e adiciona uma referência toohello [pacote de NuGet do SDK do serviço de Azure IoT].

4. Adicione o seguinte Olá `using` instrução na parte superior de saudação do hello **Program.cs** arquivo:
   
        using Microsoft.Azure.Devices;
5. Adicionar Olá toohello campos a seguir **programa** classe. Substituir valor de espaço reservado de saudação com a cadeia de conexão do hello IoT hub do [começar com o IoT Hub]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Adicionar Olá após o método toohello **programa** classe:
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Esse método envia um novo dispositivo toohello mensagem de nuvem para dispositivo com a ID de saudação `myFirstDevice`. Altere este parâmetro somente se ele tenha sido modificado de saudação usado no [começar com o IoT Hub].
7. Finalmente, adicione Olá toohello linhas a seguir **principal** método:
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. No Visual Studio, clique com o botão direito do mouse na solução e selecione **Definir Projetos de inicialização...**. Selecione **vários projetos de inicialização**, em seguida, selecione Olá **iniciar** ação para **ReadDeviceToCloudMessages**, **SimulatedDevice**, e **SendCloudToDevice**.
9. Pressione **F5**. Todos os três aplicativos devem ser iniciados. Selecione Olá **SendCloudToDevice** windows e pressione **Enter**. Você deve ver a mensagem de saudação sendo recebida pelo aplicativo de dispositivo de saudação.
   
   ![Aplicativo recebendo mensagens][21]

## <a name="receive-delivery-feedback"></a>Receber comentários de entrega
É confirmações de entrega (ou expiração) toorequest possíveis de IoT Hub para cada mensagem de nuvem para dispositivo. Essa opção permite Olá solução back-end tooeasily informam a lógica de repetição ou compensação. Para obter mais informações sobre seus comentários de nuvem para dispositivo, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].

Nesta seção, você modificar Olá **SendCloudToDevice** comentários toorequest do aplicativo e recebê-las de IoT Hub.

1. No Visual Studio, no hello **SendCloudToDevice** de projeto, adicione Olá após o método toohello **programa** classe.
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    Observe que esse padrão de recebimento é Olá mensagens de nuvem para dispositivo tooreceive usado um mesmo do aplicativo de dispositivo de saudação.
2. Adicionar Olá seguinte método em Olá **principal** método logo após Olá `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` linha:
   
        ReceiveFeedbackAsync();
3. comentários toorequest para entrega de saudação da mensagem de nuvem para dispositivo, você tem toospecify uma propriedade em Olá **SendCloudToDeviceMessageAsync** método. Adicionar Olá a seguinte linha, à direita após Olá `var commandMessage = new Message(...);` linha:
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Executar aplicativos Olá pressionando **F5**. Você deve ver todos os três aplicativos serem iniciados. Selecione Olá **SendCloudToDevice** windows e pressione **Enter**. Você deve ver Olá mensagem sendo recebidas pelo aplicativo de dispositivo hello e após alguns segundos, Olá mensagem comentários recebida pelo seu **SendCloudToDevice** aplicativo.
   
   ![Aplicativo recebendo mensagens][22]

> [!NOTE]
> Para simplificar, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].
> 
> 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toosend e receber mensagens de nuvem para dispositivo. 

exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite].

toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[pacote de NuGet do SDK do serviço de Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[guia do desenvolvedor de IoT Hub]: iot-hub-devguide.md
[começar com o IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDKs do dispositivo IoT do Azure]: iot-hub-devguide-sdks.md