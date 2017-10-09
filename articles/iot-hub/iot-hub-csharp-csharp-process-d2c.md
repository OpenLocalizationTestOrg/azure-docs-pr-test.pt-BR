---
title: mensagens de dispositivo para a nuvem do Azure IoT Hub aaaProcess usando rotas (.Net) | Microsoft Docs
description: "Como tooprocess mensagens de dispositivo para a nuvem de IoT Hub usando regras de roteamento e pontos de extremidade personalizados toodispatch mensagens tooother serviços de back-end."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>Processar mensagens do dispositivo para nuvem do Hub IoT usando rotas (.NET)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Este tutorial baseia-se em Olá [começar com o IoT Hub] tutorial. tutorial de saudação:

* Mostra como roteamento toouse as regras de mensagens de dispositivo para nuvem toodispatch de forma fácil, com base em configuração.
* Ilustra como tooisolate mensagens interativo que requerem ação imediata da solução Olá back-end para processamento adicional. Por exemplo, um dispositivo pode enviar uma mensagem de alarme que dispara e insere um tíquete em um sistema CRM. Por outro lado, as mensagens de ponto de dados, como telemetria de temperatura, são enviadas ao mecanismo de análise.

No final da saudação deste tutorial, você deve executar três aplicativos de console do .NET:

* **SimulatedDevice**, uma versão modificada do aplicativo hello criado no hello [começar com o IoT Hub] tutorial envia mensagens de dispositivo para a nuvem de ponto de dados por segundo, e mensagens de dispositivo para nuvem interativa cada 10 segundos.
* **ReadDeviceToCloudMessages** exibe Olá não críticos telemetria enviada pelo seu aplicativo de dispositivo.
* **ReadCriticalQueue** filas de mensagens críticas de saudação enviadas pelo seu aplicativo de dispositivo de uma fila do barramento de serviço. Essa fila é anexado toohello IoT hub.

> [!NOTE]
> O Hub IoT tem suporte de SDK para várias plataformas de dispositivo e linguagens, incluindo C, Java e JavaScript. toolearn como tooreplace Olá dispositivo simulado neste tutorial com um dispositivo físico, consulte Olá [Centro de desenvolvedores do Azure IoT].

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. <br/>Se você não tem uma conta, pode criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.

Você também precisa ter um conhecimento básico do [Armazenamento do Azure] e do [Barramento de Serviço do Azure].

## <a name="send-interactive-messages"></a>Enviar mensagens interativas

Modificar Olá dispositivo aplicativo que você criou no hello [começar com o IoT Hub] toooccasionally tutorial enviar mensagens interativas.

No Visual Studio, no hello **SimulatedDevice** de projeto, substitua Olá `SendDeviceToCloudMessagesAsync` método com hello código a seguir:

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

Este método adiciona aleatoriamente propriedade Olá `"level": "critical"` toomessages enviadas pelo dispositivo hello, que simula uma mensagem que requer uma ação imediata pela solução de saudação back-end. aplicativo de dispositivo Olá transmite essas informações nas propriedades de mensagem de saudação, em vez de no corpo da mensagem de saudação, para que o IoT Hub pode rotear o destino da mensagem apropriada Olá mensagem toohello.

> [!NOTE]
> Você pode usar mensagens de tooroute de propriedades de mensagem para vários cenários, incluindo frio-caminho de processamento, além de exemplo de caminho hot toohello mostrado aqui.

> [!NOTE]
> Para a mesma Olá de simplicidade, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar uma política de repetição como retirada exponencial, conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>Fila de mensagens tooa de rota em seu hub IoT

Nesta seção, você:

* Criará uma fila do Barramento de Serviço.
* Conecte-o tooyour IoT hub.
* Configure seu IoT hub toosend mensagens toohello fila com base na presença de saudação de uma propriedade na mensagem de saudação.

Para obter mais informações sobre como tooprocess mensagens das filas do barramento de serviço, consulte [começar com filas][Service Bus queue].

1. Crie uma fila do Barramento de Serviço conforme descrito em [Introdução às filas][Service Bus queue]. Olá fila deve ser no hello mesma assinatura e região, como o hub IoT. Faça uma anotação de nome de namespace e fila hello.

    > [!NOTE]
    > As filas e os tópicos do Barramento de Serviço utilizados como pontos de extremidade do Hub IoT não devem ter **Sessões** nem **Detecção Duplicada** habilitadas. Se qualquer uma dessas opções estiver habilitada, o ponto de extremidade de saudação aparece como **inacessível** em Olá portal do Azure.

2. Olá portal do Azure, abra seu hub IoT em e clique em **pontos de extremidade**.
    
    ![Pontos de extremidade no Hub IoT][30]

3. Em Olá **pontos de extremidade** folha, clique em **adicionar** em Olá tooadd superior hub IoT de tooyour de fila. O ponto de extremidade do nome hello **CriticalQueue** e usar Olá suspensas tooselect **fila do barramento de serviço**, Olá namespace de barramento de serviço no qual reside a fila e Olá nome da fila. Quando terminar, clique em **salvar** na parte inferior da saudação.
    
    ![Adicionando um ponto de extremidade][31]
    
4. Agora clique em **Rotas** no Hub IoT. Clique em **adicionar** na parte superior de saudação do hello folha toocreate uma regra de roteamento que roteia mensagens toohello fila apenas adicionada. Selecione **DeviceTelemetry** como fonte de saudação de dados. Digite `level="critical"` como condição Olá e escolha fila Olá que você acabou de adicionar como um ponto de extremidade personalizado como ponto de extremidade de regra de roteamento de saudação. Quando terminar, clique em **salvar** na parte inferior da saudação.
    
    ![Adicionando uma rota][32]
    
    Certifique-se de rota fallback hello está definida muito**ON**. Esse valor é a configuração padrão de saudação para um hub IoT.
    
    ![Rota de fallback][33]

## <a name="read-from-hello-queue-endpoint"></a>Ler a partir do ponto de extremidade de fila Olá

Nesta seção, você pode ler mensagens de saudação do ponto de extremidade de fila hello.

1. No Visual Studio, adicionar uma Visual C# Windows clássico Desktop projeto toohello solução atual, usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto. Projeto de saudação do nome **ReadCriticalQueue**.

2. No Gerenciador de soluções, clique com botão direito Olá **ReadCriticalQueue** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**. Essa operação exibe Olá **NuGet Package Manager** janela.

3. Procurar **windowsazure. ServiceBus**, clique em **instalar**e aceite os termos de uso do hello. Esta operação baixa, instala e adiciona uma referência toohello barramento de serviço do Azure, com todas as suas dependências.

4. Adicione o seguinte Olá **usando** instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. Finalmente, adicione Olá toohello linhas a seguir **principal** método. Substitua a cadeia de caracteres de conexão de saudação com **escutar** permissões para Olá fila:
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Executar aplicativos Olá
Agora você está pronto toorun aplicativos de saudação.

1. No Visual Studio, no Gerenciador de Soluções, clique com o botão direito do mouse na solução e selecione **Definir Projetos de Inicialização**. Selecione **vários projetos de inicialização**, em seguida, selecione **iniciar** como ação Olá Olá **ReadDeviceToCloudMessages**, **SimulatedDevice**, e **ReadCriticalQueue** projetos.
2. Pressione **F5** toostart Olá três aplicativos de console. Olá **ReadDeviceToCloudMessages** aplicativo tem apenas as mensagens não críticos enviadas Olá **SimulatedDevice** aplicativo e hello **ReadCriticalQueue** aplicativo tem apenas mensagens críticas.
   
   ![Três aplicativos de console][50]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como tooreliably expedir as mensagens de dispositivo para nuvem usando a funcionalidade de roteamento de mensagem de saudação do IoT Hub.

Olá [como mensagens de nuvem para dispositivo toosend com o IoT Hub] [ lnk-c2d] mostra como toosend mensagens tooyour dispositivos de back-end sua solução.

exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite][lnk-suite].

toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].

toolearn mais sobre o roteamento de mensagens no IoT Hub, consulte [enviar e receber mensagens com o IoT Hub][lnk-devguide-messaging].

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Armazenamento do Azure]: https://azure.microsoft.com/documentation/services/storage/
[Barramento de Serviço do Azure]: https://azure.microsoft.com/documentation/services/service-bus/
[guia do desenvolvedor de IoT Hub]: iot-hub-devguide.md
[começar com o IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Centro de desenvolvedores do Azure IoT]: https://azure.microsoft.com/develop/iot
[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
