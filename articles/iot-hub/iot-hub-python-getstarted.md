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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="522c2-104">Conecte seu dispositivo simulado tooyour IoT hub que usando Python</span><span class="sxs-lookup"><span data-stu-id="522c2-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="522c2-105">No final da saudação deste tutorial, você tem dois aplicativos Python:</span><span class="sxs-lookup"><span data-stu-id="522c2-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="522c2-106">**CreateDeviceIdentity.py**, que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="522c2-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="522c2-107">**SimulatedDevice.py**, que conecta tooyour hub IoT com a identidade do dispositivo Olá criada anteriormente e periodicamente envia a Telemetria da mensagem usando o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="522c2-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="522c2-108">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="522c2-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="522c2-109">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="522c2-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="522c2-110">[Python 2.x or 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="522c2-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="522c2-111">Tornar-se de que toouse Olá 32 bits ou 64 bits instalação conforme exigido pela sua configuração.</span><span class="sxs-lookup"><span data-stu-id="522c2-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="522c2-112">Quando solicitado durante a instalação de saudação, certifique-se de variável de ambiente específico da plataforma tooadd Python tooyour.</span><span class="sxs-lookup"><span data-stu-id="522c2-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="522c2-113">Se você estiver usando Python 2. x, talvez seja necessário muito[instalar ou atualizar *pip*, Python hello pacote system management][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="522c2-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="522c2-114">Se você estiver usando o sistema operacional Windows, em seguida, [pacote redistribuível do Visual C++] [ lnk-visual-c-redist] tooallow uso Olá DLLs nativas do Python.</span><span class="sxs-lookup"><span data-stu-id="522c2-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="522c2-115">[Node.js 4.0 ou posterior][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="522c2-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="522c2-116">Tornar-se de que toouse Olá 32 bits ou 64 bits instalação conforme exigido pela sua configuração.</span><span class="sxs-lookup"><span data-stu-id="522c2-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="522c2-117">Isso é necessário tooinstall Olá [ferramenta Gerenciador de Hub IoT][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="522c2-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="522c2-118">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="522c2-118">An active Azure account.</span></span> <span data-ttu-id="522c2-119">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="522c2-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="522c2-120">Olá *pip* pacotes para `azure-iothub-service-client` e `azure-iothub-device-client` estão atualmente disponíveis apenas para o sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="522c2-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="522c2-121">Para Linux/Mac OS, consulte seções Linux e específicas do sistema operacional Mac toohello Olá [preparar seu ambiente de desenvolvimento para Python] [ lnk-python-devbox] post.</span><span class="sxs-lookup"><span data-stu-id="522c2-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="522c2-122">Você criou seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="522c2-122">You have now created your IoT hub.</span></span> <span data-ttu-id="522c2-123">Use Olá nome de host do IoT Hub e hello cadeia de caracteres de conexão de IoT Hub no restante deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="522c2-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="522c2-124">Você pode também criar facilmente seu hub IoT em uma linha de comando, usando Olá Python ou Node.js com base CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="522c2-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="522c2-125">artigo Olá [criar um hub IoT usando hello Azure CLI 2.0] [ lnk-azure-cli-hub] mostra você Olá etapas rápidas toodo assim.</span><span class="sxs-lookup"><span data-stu-id="522c2-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="522c2-126">Criar uma identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="522c2-126">Create a device identity</span></span>
<span data-ttu-id="522c2-127">Esta seção lista as etapas de saudação toocreate um aplicativo de console do Python, que cria uma identidade de dispositivo no registro de identidade de saudação do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="522c2-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="522c2-128">Um dispositivo só pode se conectar a tooIoT Hub se ela possui uma entrada no registro de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="522c2-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="522c2-129">Para obter mais informações, consulte Olá **registro identidade** seção Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="522c2-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="522c2-130">Quando você executa esse aplicativo de console, ele gera uma ID de dispositivo exclusivo e chave que seu dispositivo possa usar tooidentify em si, quando ele envia o dispositivo para nuvem mensagens tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="522c2-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="522c2-131">Abra um prompt de comando e instalar Olá **Azure IoT Hub serviço SDK para Python**.</span><span class="sxs-lookup"><span data-stu-id="522c2-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="522c2-132">Feche o prompt de comando de saudação depois de instalar o SDK de saudação.</span><span class="sxs-lookup"><span data-stu-id="522c2-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="522c2-133">Crie um arquivo Python chamado **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="522c2-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="522c2-134">Abri-lo no [um editor Python/IDE de sua escolha][lnk-python-ide-list], por exemplo, Olá padrão [ocioso][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="522c2-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="522c2-135">Adicione Olá após aos módulos de código tooimport Olá necessária do SDK do serviço de saudação:</span><span class="sxs-lookup"><span data-stu-id="522c2-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="522c2-136">Adicionar Olá código a seguir, substituindo o espaço reservado de saudação para `[IoTHub Connection String]` com a cadeia de caracteres de conexão de saudação de hub IoT de saudação você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="522c2-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="522c2-137">Você pode usar qualquer nome como Olá `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="522c2-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="522c2-138">Adicionar Olá tooprint de função a seguir algumas das informações de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="522c2-138">Add hello following function tooprint some of hello device information.</span></span>

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
3. <span data-ttu-id="522c2-139">Adicione Olá identificação de dispositivo do função toocreate hello usando Olá Gerenciador de registro a seguir.</span><span class="sxs-lookup"><span data-stu-id="522c2-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

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
4. <span data-ttu-id="522c2-140">Finalmente, adicione a função principal hello da seguinte maneira e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="522c2-140">Finally, add hello main function as follows and save hello file.</span></span>

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
5. <span data-ttu-id="522c2-141">No prompt de comando hello, execute Olá **CreateDeviceIdentity.py** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="522c2-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="522c2-142">Você verá o dispositivo simulado de saudação obtendo criado.</span><span class="sxs-lookup"><span data-stu-id="522c2-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="522c2-143">Anote Olá **deviceId** e hello **primaryKey** deste dispositivo.</span><span class="sxs-lookup"><span data-stu-id="522c2-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="522c2-144">É necessário mais tarde esses valores quando você cria um aplicativo que se conecta tooIoT Hub como um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="522c2-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![Criar acesso ao dispositivo][1]

> [!NOTE]
> <span data-ttu-id="522c2-146">Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable.</span><span class="sxs-lookup"><span data-stu-id="522c2-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="522c2-147">Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="522c2-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="522c2-148">Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="522c2-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="522c2-149">Para obter mais informações, consulte Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="522c2-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="522c2-150">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="522c2-150">Create a simulated device app</span></span>
<span data-ttu-id="522c2-151">Esta seção lista Olá etapas toocreate um aplicativo de console do Python, que simula um dispositivo e envia o hub de IoT tooyour mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="522c2-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="522c2-152">Abra um prompt de comando novo e instale hello Azure IoT Hub dispositivo SDK para Python da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="522c2-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="522c2-153">Feche o prompt de comando do hello após a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="522c2-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="522c2-154">Crie um arquivo chamado **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="522c2-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="522c2-155">Abra-o em um editor/IDE do Python de sua escolha (por exemplo, OCIOSO).</span><span class="sxs-lookup"><span data-stu-id="522c2-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="522c2-156">Adicione Olá aos módulos de código tooimport Olá necessários a seguir do dispositivo Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="522c2-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="522c2-157">Adicione o seguinte Olá código e substitua o espaço reservado de saudação para `[IoTHub Device Connection String]` com a cadeia de caracteres de conexão de saudação para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="522c2-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="522c2-158">cadeia de caracteres de conexão de dispositivo Olá geralmente está no formato de saudação do `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="522c2-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="522c2-159">Saudação de uso **deviceId** e **primaryKey** do dispositivo Olá criado na Olá Olá tooreplace da seção anterior `<deviceId>` e `<primaryKey>` respectivamente.</span><span class="sxs-lookup"><span data-stu-id="522c2-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="522c2-160">Substitua `<hostName>` pelo nome do host do seu hub IoT, normalmente `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="522c2-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

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
5. <span data-ttu-id="522c2-161">Adicione Olá um retorno de chamada de confirmação de envio de toodefine de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="522c2-161">Add hello following code toodefine a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="522c2-162">Adicione saudação do cliente de dispositivo Olá código tooinitialize a seguir.</span><span class="sxs-lookup"><span data-stu-id="522c2-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="522c2-163">Adicione o seguinte Olá tooformat de função e envia uma mensagem do seu hub do dispositivo simulado tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="522c2-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

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
8. <span data-ttu-id="522c2-164">Finalmente, adicione a função principal hello.</span><span class="sxs-lookup"><span data-stu-id="522c2-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="522c2-165">Salve e feche o hello **SimulatedDevice.py** arquivo.</span><span class="sxs-lookup"><span data-stu-id="522c2-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="522c2-166">Você está agora pronto toorun este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="522c2-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="522c2-167">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="522c2-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="522c2-168">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="522c2-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="522c2-169">Receber mensagens do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="522c2-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="522c2-170">tooreceive mensagens de telemetria do seu dispositivo, você precisa toouse um [Hubs de eventos][lnk-event-hubs-overview]-compatível com ponto de extremidade exposto por Olá IoT Hub, que lê mensagens de saudação do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="522c2-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="522c2-171">Saudação de leitura [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] para obter informações sobre como tooprocess mensagens de Hubs de eventos para o ponto de extremidade de Hub de eventos-compatível com do hub IoT tutorial.</span><span class="sxs-lookup"><span data-stu-id="522c2-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="522c2-172">Hubs de eventos ainda não suporta telemetria em Python, portanto você pode criar um [Node.js](iot-hub-node-node-getstarted.md#D2C_node) ou um [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) mensagens de dispositivo para a nuvem de saudação do console baseado em Hubs de eventos aplicativo tooread de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="522c2-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="522c2-173">Este tutorial mostra como você pode usar o hello [ferramenta Gerenciador de Hub IoT] [ lnk-iot-hub-explorer] tooread essas mensagens de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="522c2-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="522c2-174">Abra um prompt de comando e instale Olá IoT Hub Explorer.</span><span class="sxs-lookup"><span data-stu-id="522c2-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="522c2-175">Executar Olá comando a seguir no prompt de comando hello, toobegin monitoramento Olá mensagens de dispositivo para a nuvem do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="522c2-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="522c2-176">Use a cadeia de caracteres de conexão do seu hub IoT no espaço reservado de saudação após `--login`.</span><span class="sxs-lookup"><span data-stu-id="522c2-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="522c2-177">Abra um novo prompt de comando e navegue toohello diretório contendo Olá **SimulatedDevice.py** arquivo.</span><span class="sxs-lookup"><span data-stu-id="522c2-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="522c2-178">Executar Olá **SimulatedDevice.py** arquivo, que envia o hub IoT do telemetria dados tooyour periodicamente.</span><span class="sxs-lookup"><span data-stu-id="522c2-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="522c2-179">Observe as mensagens de saudação do dispositivo no prompt de comando Olá executando Olá Gerenciador de Hub IoT da seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="522c2-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Mensagens do dispositivo para a nuvem de Python][2]

## <a name="next-steps"></a><span data-ttu-id="522c2-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="522c2-181">Next steps</span></span>
<span data-ttu-id="522c2-182">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="522c2-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="522c2-183">Você usou este dispositivo identidade tooenable Olá simulado dispositivo aplicativo toosend mensagens de dispositivo para nuvem toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="522c2-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="522c2-184">Mensagens de saudação recebidas pelo hub IoT de saudação com a Ajuda de saudação da ferramenta de Gerenciador de Hub IoT Olá que você observou.</span><span class="sxs-lookup"><span data-stu-id="522c2-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="522c2-185">Olá tooexplore SDK de Python para uso do Azure IoT Hub profundidade, visite [este repositório Git Hub][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="522c2-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="522c2-186">tooreview Olá recursos de mensagens de saudação do Azure IoT Hub serviço SDK para Python, você pode baixar e executar [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="522c2-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="522c2-187">Simulação do lado do dispositivo usando hello Azure IoT Hub dispositivo SDK para Python, você pode baixar e executar Olá [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="522c2-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="522c2-188">toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="522c2-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="522c2-189">[Conectando o dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="522c2-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="522c2-190">[Introdução ao gerenciamento de dispositivo][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="522c2-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="522c2-191">[Introdução ao Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="522c2-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="522c2-192">toolearn como tooextend seu IoT solução e o processo de dispositivo para nuvem mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="522c2-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
