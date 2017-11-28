---
title: "Introdução ao Hub IoT do Azure (Python) | Microsoft Docs"
description: "Saiba como enviar mensagens de dispositivo para nuvem para o Hub IoT do Azure usando os SDKs da IoT para Python. Crie um dispositivo simulado e aplicativos de serviço para registrar seu dispositivo, envie mensagens e leia mensagens no hub IoT."
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
ms.openlocfilehash: 7ebbac4464d793717f68a4cb7905c53d1f5c051a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-python"></a><span data-ttu-id="83606-104">Conecte seu dispositivo simulado ao Hub IoT usando Python</span><span class="sxs-lookup"><span data-stu-id="83606-104">Connect your simulated device to your IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="83606-105">No fim deste tutorial, você terá dois aplicativos de Python:</span><span class="sxs-lookup"><span data-stu-id="83606-105">At the end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="83606-106">**CreateDeviceIdentity.py**, que cria uma identidade do dispositivo e uma chave de segurança associada para conectar o aplicativo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="83606-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="83606-107">**SimulatedDevice.py**, que se conecta ao hub IoT com a identidade do dispositivo criada anteriormente e, periodicamente, envia uma mensagem de telemetria usando o protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="83606-107">**SimulatedDevice.py**, which connects to your IoT hub with the device identity created earlier, and periodically sends a telemetry message using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="83606-108">O artigo [SDKs de IoT do Azure][lnk-hub-sdks] fornece informações sobre os SDKs de IoT do Azure que você pode usar para criar aplicativos executados em dispositivos e no back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="83606-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="83606-109">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="83606-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="83606-110">[Python 2.x or 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="83606-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="83606-111">Certifique-se de usar a instalação de 32 bits ou 64 bits conforme exigido pelo seu programa de instalação.</span><span class="sxs-lookup"><span data-stu-id="83606-111">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="83606-112">Quando solicitado durante a instalação, certifique-se de adicionar Python à variável de ambiente específica da plataforma.</span><span class="sxs-lookup"><span data-stu-id="83606-112">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span></span> <span data-ttu-id="83606-113">Se você estiver usando o Python 2. x, talvez seja necessário [instalar ou atualizar o *pip*, o sistema de gerenciamento de pacotes do Python][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="83606-113">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="83606-114">Se você estiver usando o sistema operacional Windows, então o [Pacote redistribuível do Visual C++][lnk-visual-c-redist] permite o uso de DLLs nativas do Python.</span><span class="sxs-lookup"><span data-stu-id="83606-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span></span>
* <span data-ttu-id="83606-115">[Node.js 4.0 ou posterior][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="83606-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="83606-116">Certifique-se de usar a instalação de 32 bits ou 64 bits conforme exigido pelo seu programa de instalação.</span><span class="sxs-lookup"><span data-stu-id="83606-116">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="83606-117">Isso é necessário para instalar a [ferramenta do Gerenciador de Hub IoT][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="83606-117">This is needed to install the [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="83606-118">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="83606-118">An active Azure account.</span></span> <span data-ttu-id="83606-119">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="83606-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="83606-120">Os pacotes *pip* para `azure-iothub-service-client` e `azure-iothub-device-client` atualmente estão disponíveis apenas para o sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="83606-120">The *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="83606-121">Para Linux/Mac OS, confira as seções do Linux e Mac OS específicas na publicação [Preparação do seu ambiente de desenvolvimento para o Python][lnk-python-devbox].</span><span class="sxs-lookup"><span data-stu-id="83606-121">For Linux/Mac OS, please refer to the Linux and Mac OS-specific sections on the [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="83606-122">Você criou seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-122">You have now created your IoT hub.</span></span> <span data-ttu-id="83606-123">Use o nome de host do Hub IoT e a cadeia de conexão do Hub IoT para o restante deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="83606-123">Use the IoT Hub host name and the IoT Hub connection string in the rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="83606-124">Você também pode criar facilmente seu hub IoT em uma linha de comando, usando a CLI do Azure baseada em Python ou Node. js.</span><span class="sxs-lookup"><span data-stu-id="83606-124">You can also easily create your IoT hub on a command line, using the Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="83606-125">O artigo [Criar um hub IoT usando o Azure CLI 2.0][lnk-azure-cli-hub] mostra os passos rápidos para fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="83606-125">The article [Create an IoT hub using the Azure CLI 2.0][lnk-azure-cli-hub] shows you the quick steps to do so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="83606-126">Criar uma identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="83606-126">Create a device identity</span></span>
<span data-ttu-id="83606-127">Esta seção lista as etapas para criar um aplicativo do console do Python que cria uma identidade do dispositivo no registro de identidade em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-127">This section lists the steps to create a Python console app, that creates a device identity in the identity registry of your IoT hub.</span></span> <span data-ttu-id="83606-128">Um dispositivo só pode se conectar ao Hub IoT se tiver uma entrada no registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="83606-128">A device can only connect to IoT Hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="83606-129">Para obter mais informações, consulte a seção **"Registro de identidade"** do [Guia do Desenvolvedor do Hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="83606-129">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="83606-130">Quando você executar esse aplicativo de console, ele irá gerar uma ID e chave do dispositivo exclusivas com as quais seu dispositivo poderá identificar-se ao enviar mensagens entre o dispositivo e a nuvem para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-130">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="83606-131">Abra um prompt de comando e instale o **SDK de Serviço do Azure IoT Hub para Python**.</span><span class="sxs-lookup"><span data-stu-id="83606-131">Open a command prompt and install the **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="83606-132">Feche o prompt de comando depois de instalar o SDK.</span><span class="sxs-lookup"><span data-stu-id="83606-132">Close the command prompt after you install the SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="83606-133">Crie um arquivo Python chamado **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="83606-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="83606-134">Abra-o em [um editor/IDE do Python de sua escolha][lnk-python-ide-list], por exemplo, o padrão [OCIOSO][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="83606-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, the default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="83606-135">Adicione o código a seguir para importar os módulos necessários do SDK de serviço:</span><span class="sxs-lookup"><span data-stu-id="83606-135">Add the following code to import the required modules from the service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="83606-136">Adicione o código abaixo, substituindo o espaço reservado para `[IoTHub Connection String]` pela cadeia de conexão para o Hub IoT criada na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="83606-136">Add the following code, replacing the placeholder for `[IoTHub Connection String]` with the connection string for the IoT hub you created in the previous section.</span></span> <span data-ttu-id="83606-137">Você pode usar qualquer nome como o `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="83606-137">You can use any name as the `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="83606-138">Adicione a seguinte função para imprimir algumas das informações do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83606-138">Add the following function to print some of the device information.</span></span>

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
3. <span data-ttu-id="83606-139">Adicione a seguinte função para criar a identificação de dispositivo usando o Gerenciador de Registro.</span><span class="sxs-lookup"><span data-stu-id="83606-139">Add the following function to create the device identification using the Registry Manager.</span></span> 

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
4. <span data-ttu-id="83606-140">Finalmente, adicione a função principal da seguinte maneira e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="83606-140">Finally, add the main function as follows and save the file.</span></span>

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using the Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. <span data-ttu-id="83606-141">No prompt de comando, execute **CreateDeviceIdentity.py** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="83606-141">On the command prompt, run the **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="83606-142">Você deve ver o dispositivo simulado sendo criado.</span><span class="sxs-lookup"><span data-stu-id="83606-142">You should see the simulated device getting created.</span></span> <span data-ttu-id="83606-143">Anote o **deviceId** e a **primaryKey** desse dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83606-143">Note down the **deviceId** and the **primaryKey** of this device.</span></span> <span data-ttu-id="83606-144">Você precisará desses valores mais tarde quando criar um aplicativo que conecta o Hub IoT como um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83606-144">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

    ![Criar acesso ao dispositivo][1]

> [!NOTE]
> <span data-ttu-id="83606-146">O Registro de identidade do Hub IoT armazena apenas as identidades de dispositivo para habilitar o acesso seguro ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-146">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="83606-147">Ele armazena as IDs e as chaves do dispositivo a usar como credenciais de segurança e um sinalizador habilitado/desabilitado que você poderá usar para desabilitar o acesso de um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="83606-147">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="83606-148">Se seu aplicativo precisar armazenar outros metadados específicos do dispositivo, ele deverá usar um repositório específico do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83606-148">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="83606-149">Para saber mais, confira o [Guia de Desenvolvedor do Hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="83606-149">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="83606-150">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="83606-150">Create a simulated device app</span></span>
<span data-ttu-id="83606-151">Esta seção lista as etapas para criar um aplicativo do console do Python que simula um dispositivo e envia mensagens do dispositivo para a nuvem para o seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-151">This section lists the steps to create a Python console app, that simulates a device and sends device-to-cloud messages to your IoT hub.</span></span>

1. <span data-ttu-id="83606-152">Abra um novo prompt de comando e instale o SDK do Dipositivo do Azure IoT Hub para Python conforme a seguir.</span><span class="sxs-lookup"><span data-stu-id="83606-152">Open a new command prompt and install the Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="83606-153">Feche o prompt de comando após a instalação.</span><span class="sxs-lookup"><span data-stu-id="83606-153">Close the command prompt after the installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="83606-154">Crie um arquivo chamado **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="83606-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="83606-155">Abra-o em um editor/IDE do Python de sua escolha (por exemplo, OCIOSO).</span><span class="sxs-lookup"><span data-stu-id="83606-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="83606-156">Adicione o código a seguir para importar os módulos necessários do SDK do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83606-156">Add the following code to import the required modules from the device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="83606-157">Adicione o código a seguir e substitua o espaço reservado por `[IoTHub Device Connection String]` pela cadeia de conexão para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83606-157">Add the following code and replace the placeholder for `[IoTHub Device Connection String]` with the connection string for your device.</span></span> <span data-ttu-id="83606-158">A cadeia de conexão do dispositivo normalmente está no formato `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="83606-158">The device connection string is usually in the format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="83606-159">Use o **deviceId** e a **primaryKey** do dispositivo que você criou na seção anterior para substituir `<deviceId>` e `<primaryKey>` respectivamente.</span><span class="sxs-lookup"><span data-stu-id="83606-159">Use the **deviceId** and **primaryKey** of the device you created in the previous section to replace the `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="83606-160">Substitua `<hostName>` pelo nome do host do seu hub IoT, normalmente `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="83606-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

    ```python
    # String containing Hostname, Device Id & Device Key in the format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. <span data-ttu-id="83606-161">Adicione o seguinte código para definir um retorno de chamada de confirmação de envio.</span><span class="sxs-lookup"><span data-stu-id="83606-161">Add the following code to define a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="83606-162">Adicione o seguinte código para inicializar o cliente do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83606-162">Add the following code to initialize the device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set the time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="83606-163">Adicione a seguinte função para formatar e enviar uma mensagem do dispositivo simulado em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-163">Add the following function to format and send a message from your simulated device to your IoT hub.</span></span>

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C to exit" )
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
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission to IoT Hub." % message_counter )

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
8. <span data-ttu-id="83606-164">Finalmente, adicione a função principal.</span><span class="sxs-lookup"><span data-stu-id="83606-164">Finally, add the main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using the Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="83606-165">Salve e feche o arquivo **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="83606-165">Save and close the **SimulatedDevice.py** file.</span></span> <span data-ttu-id="83606-166">Agora você está pronto para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83606-166">You are now ready to run this app.</span></span>

> [!NOTE]
> <span data-ttu-id="83606-167">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="83606-167">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="83606-168">No código de produção, implemente políticas de repetição (como uma retirada exponencial), como sugerido no artigo [Tratamento de falhas transitórias][lnk-transient-faults] do MSDN.</span><span class="sxs-lookup"><span data-stu-id="83606-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="83606-169">Receber mensagens do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="83606-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="83606-170">Para receber mensagens de telemetria do seu dispositivo, você precisa usar um ponto de extremidade compatível com [Hubs de eventos][lnk-event-hubs-overview] exposto pelo Hub IoT, que lê as mensagens do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="83606-170">To receive telemetry messages from your device, you need to use an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by the IoT Hub, which reads the device-to-cloud messages.</span></span> <span data-ttu-id="83606-171">Leia o tutorial [Introdução aos Hubs de Eventos][lnk-eventhubs-tutorial] para saber informações sobre como processar as mensagens dos Hubs de Eventos para o ponto de extremidade compatível com o Hub de Eventos do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-171">Read the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how to process messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="83606-172">Os Hubs de Eventos não suportam telemetria em Python, então você pode criar um [Node. js](iot-hub-node-node-getstarted.md#D2C_node) ou um aplicativo de console baseado em Hubs de Eventos do [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) para ler as mensagens do dispositivo para a nuvem de Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app to read the device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="83606-173">Este tutorial mostra como você pode usar a [ferramenta Gerenciador de Hub IoT][lnk-iot-hub-explorer] para ler essas mensagens de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83606-173">This tutorial shows how you can use the [IoT Hub Explorer tool][lnk-iot-hub-explorer] to read these device messages.</span></span>

1. <span data-ttu-id="83606-174">Abra um prompt de comando e instale o Gerenciador de Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-174">Open a command prompt and install the IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="83606-175">Execute o seguinte comando no prompt de comando, para começar a monitorar as mensagens do dispositivo para a nuvem a partir do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83606-175">Run the following command on the command prompt, to begin monitoring the device-to-cloud messages from your device.</span></span> <span data-ttu-id="83606-176">Use a cadeia de conexão do seu hub IoT no espaço reservado após `--login`.</span><span class="sxs-lookup"><span data-stu-id="83606-176">Use your IoT hub's connection string in the placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="83606-177">Abra um novo prompt de comando e navegue até o diretório que contém o arquivo **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="83606-177">Open a new command prompt and navigate to the directory containing the **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="83606-178">Execute o arquivo **SimulatedDevice.py**, que envia periodicamente os dados de telemetria para o seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-178">Run the **SimulatedDevice.py** file, which periodically sends telemetry data to your IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="83606-179">Observe as mensagens de dispositivo no prompt de comando executando o Gerenciador de Hub IoT da seção anterior.</span><span class="sxs-lookup"><span data-stu-id="83606-179">Observe the device messages on the command prompt running the IoT Hub Explorer from the previous section.</span></span> 

    ![Mensagens do dispositivo para a nuvem de Python][2]

## <a name="next-steps"></a><span data-ttu-id="83606-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83606-181">Next steps</span></span>
<span data-ttu-id="83606-182">Neste tutorial, você configurou um novo hub IoT no portal do Azure e depois criou uma identidade do dispositivo no Registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-182">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="83606-183">Você usou essa identidade do dispositivo para habilitar o aplicativo de dispositivo simulado para enviar as mensagens entre o dispositivo e a nuvem para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-183">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="83606-184">Você observou as mensagens recebidas pelo hub IoT com a Ajuda da ferramenta do Gerenciador de Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="83606-184">You observed the messages received by the IoT hub with the help of the IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="83606-185">Para explorar o SDK do Python para uso do Hub IoT do Azure em detalhes, visite [este repositório do Git Hub][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="83606-185">To explore the Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="83606-186">Para examinar os recursos de mensagens do SDK de serviço do Hub IoT do Azure para Python, você pode baixar e executar [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="83606-186">To review the messaging capabilities of the Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="83606-187">Para a simulação do lado do dispositivo usando o SDK do dispositivo de Hub IoT do Azure para Python, você pode baixar e executar [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="83606-187">For device side simulation using the Azure IoT Hub Device SDK for Python, you can download and run the [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="83606-188">Para continuar a introdução ao Hub IoT e explorar outros cenários de IoT, confira:</span><span class="sxs-lookup"><span data-stu-id="83606-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="83606-189">[Conectando o dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="83606-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="83606-190">[Introdução ao gerenciamento de dispositivo][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="83606-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="83606-191">[Introdução ao Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="83606-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="83606-192">Para saber como estender sua solução IoT e processar as mensagens entre o dispositivo e a nuvem em escala, consulte o tutorial [Processar as mensagens entre o dispositivo e a nuvem][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="83606-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
