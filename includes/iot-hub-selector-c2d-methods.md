> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

O Hub IoT do Azure é um serviço totalmente gerenciado que permite comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end da solução. Tutoriais anteriores ([começar com o IoT Hub] e [enviar mensagens de nuvem para dispositivo com o IoT Hub]) ilustram Olá dispositivo para nuvem e nuvem para dispositivo mensagens funcionalidade básica de IoT Hub. IoT Hub também lhe Olá métodos de não duráveis tooinvoke capacidade nos dispositivos da nuvem de saudação. Direcionar métodos representam uma interação de solicitação-resposta com um tooan semelhante dispositivo HTTP chamadas em que elas foram bem-sucedidas ou falham imediatamente (após um tempo limite especificado pelo usuário) o usuário de saudação do toolet saber status saudação da chamada de saudação. [Invocar um método direto em um dispositivo] [ lnk-devguide-methods] descreve métodos diretos em mais detalhes e oferece orientação sobre quando toouse direciona métodos em vez de mensagens de nuvem para dispositivo ou propriedades desejadas.

Este tutorial mostra como:

* Use Olá toocreate portal do Azure um hub IoT e criar uma identidade de dispositivo em seu hub IoT.
* Crie um aplicativo de dispositivo simulado que tem um método que pode ser chamado por nuvem hello.
* Crie um aplicativo de console que chama um método direto no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.

> [!NOTE]
> Neste momento, métodos diretos são somente com suporte em dispositivos que se conectam usando o Hub tooIoT Olá protocolo MQTT. Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como tooconvert existente dispositivo aplicativo toouse MQTT.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[enviar mensagens de nuvem para dispositivo com o IoT Hub]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[começar com o IoT Hub]: ../articles/iot-hub/iot-hub-node-node-getstarted.md