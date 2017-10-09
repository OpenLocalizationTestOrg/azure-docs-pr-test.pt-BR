> [!div class="op_single_selector"]
> * [Dispositivo: Node.js Serviço: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Dispositivo: Node.js Serviço: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Dispositivo: serviço de Java: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Aplicativos de back-end podem usar tipos primitivos Azure IoT Hub, como [duas dispositivo] [ lnk-devtwin] e [direto métodos][lnk-c2dmethod], tooremotely iniciar e monitorar ações de gerenciamento de dispositivo nos dispositivos. Este tutorial mostra como um aplicativo de back-end e um aplicativo de dispositivo podem trabalhar juntos tooinitiate e monitorar uma reinicialização do dispositivo remoto usando o IoT Hub.

Use as ações de gerenciamento de dispositivo um método direto tooinitiate (como reinicialização, redefinição de fábrica e atualização de firmware) de um aplicativo de back-end na nuvem de saudação. dispositivo de saudação é responsável por:

* Tratamento de solicitação do método hello enviada do IoT Hub.
* Iniciando ação no dispositivo de saudação do hello correspondente específico do dispositivo.
* Fornecendo atualizações de status por meio de *relatado propriedades* tooIoT Hub.

Você pode usar um aplicativo de back-end em Olá nuvem toorun dispositivo duas consultas tooreport em andamento Olá de suas ações de gerenciamento de dispositivo.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
