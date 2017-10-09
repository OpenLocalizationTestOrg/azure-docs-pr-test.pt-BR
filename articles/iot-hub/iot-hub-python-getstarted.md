---
title: "aaaGet de Introdução ao Azure IoT Hub (Python) | Microsoft Docs"
description: "Saiba como dispositivo para nuvem toosend mensagens tooAzure IoT Hub usando IoT SDKs para Python. Criar dispositivo simulado e tooregister de aplicativos de serviço de seu dispositivo, enviar mensagens e ler mensagens de hub IoT."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Conecte seu dispositivo simulado tooyour IoT hub que usando Python
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

No final da saudação deste tutorial, você tem dois aplicativos Python:

* **CreateDeviceIdentity.py**, que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo simulado.
* **SimulatedDevice.py**, que conecta tooyour hub IoT com a identidade do dispositivo Olá criada anteriormente e periodicamente envia a Telemetria da mensagem usando o protocolo MQTT hello.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.
> 
> 

toocomplete neste tutorial, você precisa Olá a seguir:

* [Python 2.x or 3.x][lnk-python-download]. Tornar-se de que toouse Olá 32 bits ou 64 bits instalação conforme exigido pela sua configuração. Quando solicitado durante a instalação de saudação, certifique-se de variável de ambiente específico da plataforma tooadd Python tooyour. Se você estiver usando Python 2. x, talvez seja necessário muito[instalar ou atualizar *pip*, Python hello pacote system management][lnk-install-pip].
* Se você estiver usando o sistema operacional Windows, em seguida, [pacote redistribuível do Visual C++] [ lnk-visual-c-redist] tooallow uso Olá DLLs nativas do Python.
* [Node.js 4.0 ou posterior][lnk-node-download]. Tornar-se de que toouse Olá 32 bits ou 64 bits instalação conforme exigido pela sua configuração. Isso é necessário tooinstall Olá [ferramenta Gerenciador de Hub IoT][lnk-iot-hub-explorer].
* Uma conta ativa do Azure. Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.

> [!NOTE]
> Olá *pip* pacotes para `azure-iothub-service-client` e `azure-iothub-device-client` estão atualmente disponíveis apenas para o sistema operacional Windows. Para Linux/Mac OS, consulte seções Linux e específicas do sistema operacional Mac toohello Olá [preparar seu ambiente de desenvolvimento para Python] [ lnk-python-devbox] post.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Você criou seu Hub IoT. Use Olá nome de host do IoT Hub e hello cadeia de caracteres de conexão de IoT Hub no restante deste tutorial hello.

> [!NOTE]
> Você pode também criar facilmente seu hub IoT em uma linha de comando, usando Olá Python ou Node.js com base CLI do Azure. artigo Olá [criar um hub IoT usando hello Azure CLI 2.0] [ lnk-azure-cli-hub] mostra você Olá etapas rápidas toodo assim. 
> 

## <a name="create-a-device-identity"></a>Criar uma identidade do dispositivo
Esta seção lista as etapas de saudação toocreate um aplicativo de console do Python, que cria uma identidade de dispositivo no registro de identidade de saudação do seu hub IoT. Um dispositivo só pode se conectar a tooIoT Hub se ela possui uma entrada no registro de identidade hello. Para obter mais informações, consulte Olá **registro identidade** seção Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity]. Quando você executa esse aplicativo de console, ele gera uma ID de dispositivo exclusivo e chave que seu dispositivo possa usar tooidentify em si, quando ele envia o dispositivo para nuvem mensagens tooIoT Hub.

1. Abra um prompt de comando e instalar Olá **Azure IoT Hub serviço SDK para Python**. Feche o prompt de comando de saudação depois de instalar o SDK de saudação.

    ```
    pip install azure-iothub-service-client
    ```

2. Crie um arquivo Python chamado **CreateDeviceIdentity.py**. Abri-lo no [um editor Python/IDE de sua escolha][lnk-python-ide-list], por exemplo, Olá padrão [ocioso][lnk-idle].

3. Adicione Olá após aos módulos de código tooimport Olá necessária do SDK do serviço de saudação:

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Adicionar Olá código a seguir, substituindo o espaço reservado de saudação para `[IoTHub Connection String]` com a cadeia de caracteres de conexão de saudação de hub IoT de saudação você criou na seção anterior hello. Você pode usar qualquer nome como Olá `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Adicionar Olá tooprint de função a seguir algumas das informações de dispositivo de saudação.

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. Adicione Olá identificação de dispositivo do função toocreate hello usando Olá Gerenciador de registro a seguir. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. Finalmente, adicione a função principal hello da seguinte maneira e salve o arquivo hello.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. No prompt de comando hello, execute Olá **CreateDeviceIdentity.py** da seguinte maneira:

    ```python
    python CreateDeviceIdentity.py
    ```
6. Você verá o dispositivo simulado de saudação obtendo criado. Anote Olá **deviceId** e hello **primaryKey** deste dispositivo. É necessário mais tarde esses valores quando você cria um aplicativo que se conecta tooIoT Hub como um dispositivo.

    ![Criar acesso ao dispositivo][1]

> [!NOTE]
> Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable. Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual. Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo. Para obter mais informações, consulte Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Esta seção lista Olá etapas toocreate um aplicativo de console do Python, que simula um dispositivo e envia o hub de IoT tooyour mensagens de dispositivo para a nuvem.

1. Abra um prompt de comando novo e instale hello Azure IoT Hub dispositivo SDK para Python da seguinte maneira. Feche o prompt de comando do hello após a instalação de saudação.

    ```
    pip install azure-iothub-device-client
    ```
2. Crie um arquivo chamado **SimulatedDevice.py**. Abra-o em um editor/IDE do Python de sua escolha (por exemplo, OCIOSO).

3. Adicione Olá aos módulos de código tooimport Olá necessários a seguir do dispositivo Olá SDK.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Adicione o seguinte Olá código e substitua o espaço reservado de saudação para `[IoTHub Device Connection String]` com a cadeia de caracteres de conexão de saudação para seu dispositivo. cadeia de caracteres de conexão de dispositivo Olá geralmente está no formato de saudação do `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Saudação de uso **deviceId** e **primaryKey** do dispositivo Olá criado na Olá Olá tooreplace da seção anterior `<deviceId>` e `<primaryKey>` respectivamente. Substitua `<hostName>` pelo nome do host do seu hub IoT, normalmente `<IoT hub name>.azure-devices.net`.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. Adicione Olá um retorno de chamada de confirmação de envio de toodefine de código a seguir. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. Adicione saudação do cliente de dispositivo Olá código tooinitialize a seguir.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Adicione o seguinte Olá tooformat de função e envia uma mensagem do seu hub do dispositivo simulado tooyour IoT.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. Finalmente, adicione a função principal hello. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Salve e feche o hello **SimulatedDevice.py** arquivo. Você está agora pronto toorun este aplicativo.

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Receber mensagens do dispositivo simulado
tooreceive mensagens de telemetria do seu dispositivo, você precisa toouse um [Hubs de eventos][lnk-event-hubs-overview]-compatível com ponto de extremidade exposto por Olá IoT Hub, que lê mensagens de saudação do dispositivo para a nuvem. Saudação de leitura [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] para obter informações sobre como tooprocess mensagens de Hubs de eventos para o ponto de extremidade de Hub de eventos-compatível com do hub IoT tutorial. Hubs de eventos ainda não suporta telemetria em Python, portanto você pode criar um [Node.js](iot-hub-node-node-getstarted.md#D2C_node) ou um [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) mensagens de dispositivo para a nuvem de saudação do console baseado em Hubs de eventos aplicativo tooread de IoT Hub. Este tutorial mostra como você pode usar o hello [ferramenta Gerenciador de Hub IoT] [ lnk-iot-hub-explorer] tooread essas mensagens de dispositivo.

1. Abra um prompt de comando e instale Olá IoT Hub Explorer. 

    ```
    npm install -g iothub-explorer
    ```

2. Executar Olá comando a seguir no prompt de comando hello, toobegin monitoramento Olá mensagens de dispositivo para a nuvem do dispositivo. Use a cadeia de caracteres de conexão do seu hub IoT no espaço reservado de saudação após `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Abra um novo prompt de comando e navegue toohello diretório contendo Olá **SimulatedDevice.py** arquivo.

4. Executar Olá **SimulatedDevice.py** arquivo, que envia o hub IoT do telemetria dados tooyour periodicamente. 
   
    ```
    python SimulatedDevice.py
    ```
5. Observe as mensagens de saudação do dispositivo no prompt de comando Olá executando Olá Gerenciador de Hub IoT da seção anterior hello. 

    ![Mensagens do dispositivo para a nuvem de Python][2]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você usou este dispositivo identidade tooenable Olá simulado dispositivo aplicativo toosend mensagens de dispositivo para nuvem toohello hub IoT. Mensagens de saudação recebidas pelo hub IoT de saudação com a Ajuda de saudação da ferramenta de Gerenciador de Hub IoT Olá que você observou. 

Olá tooexplore SDK de Python para uso do Azure IoT Hub profundidade, visite [este repositório Git Hub][lnk-python-github]. tooreview Olá recursos de mensagens de saudação do Azure IoT Hub serviço SDK para Python, você pode baixar e executar [iothub_messaging_sample.py][lnk-messaging-sample]. Simulação do lado do dispositivo usando hello Azure IoT Hub dispositivo SDK para Python, você pode baixar e executar Olá [iothub_client_sample.py][lnk-client-sample].

toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Conectando o dispositivo][lnk-connect-device]
* [Introdução ao gerenciamento de dispositivo][lnk-device-management]
* [Introdução ao Azure IoT Edge][lnk-iot-edge]

toolearn como tooextend seu IoT solução e o processo de dispositivo para nuvem mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
