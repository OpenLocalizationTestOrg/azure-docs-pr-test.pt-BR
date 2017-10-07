---
title: aaaProcess mensagens de dispositivo para a nuvem do Azure IoT Hub (Java) | Microsoft Docs
description: "Como tooprocess mensagens de dispositivo para a nuvem de IoT Hub usando regras de roteamento e pontos de extremidade personalizados toodispatch mensagens tooother serviços de back-end."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>Processar mensagens do Hub IoT do dispositivo para nuvem (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

O Hub IoT do Azure é um serviço totalmente gerenciado que permite comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end da solução. Outros tutoriais ([começar com o IoT Hub] e [enviar mensagens de nuvem para dispositivo com o IoT Hub][lnk-c2d]) mostram como toouse Olá básica dispositivo para nuvem e nuvem para dispositivo funcionalidade de mensagens do IoT Hub.

Este tutorial baseia-se em código Olá mostrado a saudação [começar com o IoT Hub] tutorial e mostra como toouse mensagem roteamento tooprocess de mensagens de dispositivo para a nuvem de forma escalonável. tutorial de saudação ilustra como tooprocess mensagens que requerem ação imediata da solução Olá back-end. Por exemplo, um dispositivo pode enviar uma mensagem de alarme que dispara e insere um tíquete em um sistema CRM. Por outro lado, as mensagens de ponto de dados simplesmente são alimentadas no mecanismo de análise. Por exemplo, a telemetria de temperatura de um dispositivo que é toobe armazenado para análise posterior é uma mensagem de ponto de dados.

No final da saudação deste tutorial, você deve executar três aplicativos de console de Java:

* **dispositivo simulado**, uma versão modificada do aplicativo hello criado no hello [começar com o IoT Hub] tutorial, envia mensagens de dispositivo para a nuvem de ponto de dados por segundo, e mensagens de dispositivo para nuvem interativa cada 10 segundos. Esse aplicativo usa Olá AMQP protocolo toocommunicate com o IoT Hub.
* **mensagens de d2c leitura** exibe telemetria Olá enviada pelo seu aplicativo de dispositivo.
* **leitura crítica fila** filas de mensagens de saudação crítico de saudação do barramento do serviço fila anexada toohello hub IoT.

> [!NOTE]
> O Hub IoT tem suporte de SDK para várias plataformas de dispositivo e linguagens, incluindo C, Java e JavaScript. Para obter instruções sobre como tooreplace Olá dispositivo neste tutorial com um dispositivo físico, e como tooconnect dispositivos tooan IoT Hub, consulte Olá [Centro de desenvolvedores do Azure IoT].

toocomplete neste tutorial, você precisa Olá a seguir:

* Uma versão completa do trabalho de saudação [começar com o IoT Hub] tutorial.
* Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Uma conta ativa do Azure. (Se você não possui uma conta, é possível criar uma [conta gratuita] [lnk-free-trial] em apenas alguns minutos.)

Você também precisa ter um conhecimento básico do [Armazenamento do Azure] e do [Barramento de Serviço do Azure].

## <a name="send-interactive-messages-from-a-device-app"></a>Enviar mensagens interativas de um aplicativo de dispositivo
Nesta seção, você modificar Olá dispositivo aplicativo que você criou no hello [começar com o IoT Hub] toooccasionally tutorial enviar mensagens que exigem processamento imediato.

1. Use um arquivo de simulated-device\src\main\java\com\mycompany\app\App.java texto editor tooopen hello. Esse arquivo contém código Olá Olá **dispositivo simulado** aplicativo que você criou no hello [começar com o IoT Hub] tutorial.

2. Substituir saudação **MessageSender** classe com hello código a seguir:

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    Este método adiciona aleatoriamente propriedade Olá `"level": "critical"` toomessages enviadas pelo dispositivo hello, que simula uma mensagem que requer uma ação imediata pelo back-end do aplicativo hello. aplicativo Hello transmite essas informações nas propriedades de mensagem de saudação, em vez de no corpo da mensagem de saudação, para que o IoT Hub pode rotear o destino da mensagem apropriada Olá mensagem toohello.
   
   > [!NOTE]
   > Você pode usar mensagens de tooroute de propriedades de mensagem para vários cenários, incluindo frio-caminho de processamento, além de exemplo de afunilamento toohello mostrado aqui.

2. Salve e feche o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java hello.

    > [!NOTE]
    > Para a mesma Olá de simplicidade, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar uma política de repetição como retirada exponencial, conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].

3. Olá toobuild **dispositivo simulado** aplicativo usando o Maven, executar Olá comando no prompt de comando Olá na pasta do dispositivo simulado Olá a seguir:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>Adicionar uma IoT de tooyour fila em hub e rota a tooit mensagens

Nesta seção, você cria uma fila do barramento de serviço, conectá-lo tooyour IoT hub e configurar seu IoT hub toosend mensagens toohello fila com base na presença de saudação de uma propriedade na mensagem de saudação. Para obter mais informações sobre como tooprocess mensagens das filas do barramento de serviço, consulte [começar com filas][lnk-sb-queues-java].

1. Crie uma fila do Barramento de Serviço conforme descrito em [Introdução às filas][lnk-sb-queues-java]. Faça uma anotação de nome de namespace e fila hello.

2. Olá portal do Azure, abra seu hub IoT em e clique em **pontos de extremidade**.

    ![Pontos de extremidade no Hub IoT][30]

3. Em Olá **pontos de extremidade** folha, clique em **adicionar** em Olá tooadd superior hub IoT de tooyour de fila. O ponto de extremidade do nome hello **CriticalQueue** e usar Olá suspensas tooselect **fila do barramento de serviço**, Olá namespace de barramento de serviço no qual reside a fila e Olá nome da fila. Quando terminar, clique em **salvar** na parte inferior da saudação.

    ![Adicionando um ponto de extremidade][31]

4. Agora clique em **Rotas** no Hub IoT. Clique em **adicionar** na parte superior de saudação do hello folha toocreate uma regra de roteamento que roteia mensagens toohello fila apenas adicionada. Selecione **DeviceTelemetry** como fonte de saudação de dados. Digite `level="critical"` como condição Olá e escolha fila Olá que você acabou de adicionar como um ponto de extremidade personalizado como ponto de extremidade de regra de roteamento de saudação. Quando terminar, clique em **salvar** na parte inferior da saudação.

    ![Adicionando uma rota][32]

    Certifique-se de rota fallback hello está definida muito**ON**. Essa configuração é a configuração padrão de saudação de um hub IoT.

    ![Rota de fallback][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(Opcional) Ler a partir do ponto de extremidade de fila Olá

Opcionalmente, você pode ler mensagens de saudação do ponto de extremidade de fila Olá, seguindo as instruções de saudação do [começar com filas][lnk-sb-queues-java]. Nome hello aplicativo **leitura crítica fila**.

## <a name="run-hello-applications"></a>Executar aplicativos Olá

Agora você está três aplicativos de saudação de toorun pronto.

1. Olá toorun **mensagens de d2c leitura** aplicativo, em um prompt de comando ou o shell navegue toohello leitura d2c pasta e executar Olá comando a seguir:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Executar read-d2c-messages][readd2c]

2. Olá toorun **leitura crítica fila** aplicativo, em um prompt de comando ou o shell de navegar a pasta de leitura crítica fila toohello e execute Olá comando a seguir:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Executar read-critical-messages][readqueue]

3. Olá toorun **dispositivo simulado** aplicativo, em um prompt de comando ou o shell navegue pasta do dispositivo simulado toohello e executar Olá comando a seguir:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Executar simulated-device][simulateddevice]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como tooreliably expedir as mensagens de dispositivo para nuvem usando a funcionalidade de roteamento de mensagem de saudação do IoT Hub.

Olá [como mensagens de nuvem para dispositivo toosend com o IoT Hub] [ lnk-c2d] mostra como toosend mensagens tooyour dispositivos de back-end sua solução.

exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite][lnk-suite].

toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].

toolearn mais sobre o roteamento de mensagens no IoT Hub, consulte [enviar e receber mensagens com o IoT Hub][lnk-devguide-messaging].

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Armazenamento do Azure]: https://azure.microsoft.com/documentation/services/storage/
[Barramento de Serviço do Azure]: https://azure.microsoft.com/documentation/services/service-bus/

[guia do desenvolvedor de IoT Hub]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[começar com o IoT Hub]: iot-hub-java-java-getstarted.md
[Centro de desenvolvedores do Azure IoT]: https://azure.microsoft.com/develop/iot
[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Tratamento de Falhas Transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
