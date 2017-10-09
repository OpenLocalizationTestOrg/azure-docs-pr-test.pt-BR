> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

Dispositivos gêmeos são documentos JSON que armazenam informações do estado do dispositivo (metadados, configurações e condições). IoT Hub mantém duas um dispositivo de cada dispositivo que se conecta tooit.

Use os dispositivos gêmeos para:

* Armazene os metadados de dispositivo de seu back-end da solução.
* Relatar informações do estado atual como recursos disponíveis e condições (por exemplo, conectividade método hello usado) de seu aplicativo de dispositivo.
* Sincronize o estado de saudação de fluxos de trabalho de longa execução (como atualizações de firmware e configuração) entre um aplicativo de dispositivo e um aplicativo de back-end.
* Consultar os metadados, a configuração ou o estado do seu dispositivo.

> [!NOTE]
> Dispositivos gêmeos são projetados para sincronização e para consultar condições e configurações de dispositivos. Para obter mais informações sobre quando toouse twins de dispositivo podem ser encontrados na [entender twins dispositivo][lnk-twins].

Dispositivos gêmeos são armazenados em um hub IoT e contêm:

* *marcas*, metadados de dispositivo acessível somente por Olá solução back-end;
* *propriedades desejadas*, objetos JSON pode ser modificados por solução Olá fazer final e observável pelo aplicativo de dispositivo Olá; e
* *relatado propriedades*, objetos JSON modificáveis pelo aplicativo de dispositivo hello e legíveis pelo back-end de solução hello. Marcas e propriedades não podem conter matrizes, mas objetos podem ser aninhados.

![][img-twin]

Além disso, back-end de solução Olá pode consultar twins de dispositivo com base em todos os Olá acima de dados.
Consulte também[entender twins dispositivo] [ lnk-twins] para obter mais informações sobre twins de dispositivo e toohello [linguagem de consulta de IoT Hub] [ lnk-query] referência para consultar.

> [!NOTE]
> Neste momento, twins de dispositivo são acessíveis somente de dispositivos que se conectam tooIoT Hub usando o protocolo MQTT hello. Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como tooconvert existente dispositivo aplicativo toouse MQTT.

Este tutorial mostra como:

* Criar um aplicativo de back-end que adiciona *marcas* tooa duas de dispositivo e um aplicativo de dispositivo simulado que relata a conectividade do canal como um *relatado propriedade* em duas de dispositivo de saudação.
* Consultar dispositivos de seu aplicativo de back-end usando filtros nas marcas de saudação e propriedades criadas anteriormente.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md