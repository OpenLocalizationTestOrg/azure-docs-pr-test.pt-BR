> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

Este passo a passo de saudação [exemplo nuvem de dispositivo simulado carregar] mostra como toouse [Azure IoT borda] [ lnk-sdk] toosend telemetria do dispositivo para nuvem tooIoT Hub de simulados dispositivos.

Este passo a passo aborda:

* **Arquitetura**: informações arquitetônicas sobre Olá [exemplo nuvem de dispositivo simulado carregar].
* **Compilar e executar**: Olá etapas necessárias toobuild e exemplo hello execução.

## <a name="architecture"></a>Arquitetura

Olá [exemplo nuvem de dispositivo simulado carregar] mostra como toocreate um gateway que envia a telemetria de simulados hub de IoT tooan dispositivos. Um dispositivo pode não ser capaz de tooconnect diretamente tooIoT Hub como dispositivo hello:

* Não usa um protocolo de comunicação compreendido pelo Hub IoT.
* Não é suficientemente inteligente tooremember Olá identidade atribuída tooit pelo IoT Hub.

Um gateway de extremidade IoT pode resolver esses problemas em Olá maneiras a seguir:

* Olá gateway compreende o protocolo de saudação usado pelo dispositivo Olá, recebe a telemetria do dispositivo para a nuvem de dispositivo de saudação e encaminha tooIoT essas mensagens Hub usando um protocolo entendido pelo hub IoT de saudação.

* gateway Olá mapeia toodevices de identidades de IoT Hub e atua como um proxy quando um dispositivo envia mensagens tooIoT Hub.

Olá diagrama a seguir mostra Olá componentes principais do exemplo hello, incluindo Olá módulos IoT borda:

![][1]

módulos de saudação não passar mensagens diretamente tooeach outros. módulos de saudação publicar mensagens tooan interno agente que oferece toohello de mensagens de saudação outros módulos usando um mecanismo de assinatura. Para obter mais informações, consulte [Introdução ao Edge IoT do Azure][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Módulo de ingestão de protocolo

Esse módulo é hello ponto de partida para receber dados de dispositivos, por meio do gateway hello e em nuvem hello. No exemplo hello, Olá módulo:

1. Cria dados de temperatura simulados. Se você usar dispositivos físicos, o módulo Olá lê os dados desses dispositivos físicos.
1. Cria uma mensagem.
1. Coloca os dados de temperatura de saudação simulada no conteúdo da mensagem de saudação.
1. Adiciona uma propriedade com uma falsa mensagem de toohello de endereço MAC.
1. Torna o próximo módulo do hello mensagem toohello disponíveis na cadeia de saudação.

módulo Olá chamado **ingestão de protocolo X** em Olá diagrama anterior é chamado **dispositivo simulado** no código-fonte hello.

### <a name="mac-lt-gt-iot-hub-id-module"></a>Módulo de identificação do MAC &lt;-&gt; Hub IoT

Este módulo procura mensagens que tenham uma propriedade de endereço Mac. No exemplo hello, módulo de inclusão de protocolo hello adiciona propriedade do endereço MAC hello. Se o módulo de saudação encontrar essa propriedade, ele adiciona outra propriedade com uma mensagem de chave toohello de dispositivo IoT Hub. módulo de Hello, em seguida, faz o próximo módulo do hello mensagem toohello disponíveis na cadeia de saudação.

desenvolvedor Olá configura um mapeamento entre endereços MAC e dispositivos do IoT Hub identidades tooassociate Olá simulado com identidades de dispositivo IoT Hub. desenvolvedor Olá adiciona mapeamento Olá manualmente como parte da configuração do módulo de saudação.

> [!NOTE]
> Esta amostra usa um endereço MAC como um identificador de dispositivo exclusivo e o correlaciona com uma identidade de dispositivo Hub IoT. No entanto, é possível escrever seu próprio módulo que usa um identificador exclusivo diferente. Por exemplo, os dispositivos podem ter números de série exclusivos ou dados de telemetria Olá podem incluir um nome de dispositivo incorporado exclusivo.

### <a name="iot-hub-communication-module"></a>Módulo de comunicação do Hub IoT

Este módulo usa mensagens com um IoT Hub propriedade de chave de dispositivo que foi atribuída pelo módulo de saudação anterior. módulo de saudação envia a mensagem de saudação tooIoT conteúdo Hub usando Olá protocolo HTTP. HTTP é uma saudação três protocolos entendidos pelo IoT Hub.

Em vez de abrir uma conexão para cada dispositivo simulado, esse módulo abre uma conexão HTTP único de hub IoT do hello gateway toohello. módulo de saudação multiplexes, em seguida, conexões de todos os dispositivos de saudação simulada por essa conexão. Essa abordagem permite que um único gateway tooconnect muitos mais dispositivos.

## <a name="before-you-get-started"></a>Antes de começar

Antes de começar, é necessário:

* [Criar um hub IoT] [ lnk-create-hub] na sua assinatura do Azure, você precisará Olá nome do seu hub toocomplete este passo a passo. Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* Adicione dois dispositivos tooyour IoT hub e anote seus ids e chaves de dispositivo. Você pode usar o hello [explorer dispositivo] [ lnk-device-explorer] ou [Gerenciador de Hub IOT] [ lnk-iothub-explorer] ferramenta tooadd seu hub IoT de toohello de dispositivos criada na Olá anterior etapa e recuperar suas chaves.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[exemplo nuvem de dispositivo simulado carregar]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md