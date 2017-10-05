---
title: Entender o suporte do MQTT do Hub IoT do Azure | Microsoft Docs
description: "Guia do desenvolvedor ‑ suporte para dispositivos que se conectam a um ponto de extremidade do Hub IoT voltado para o dispositivo usando o protocolo MQTT. Inclui informações sobre suporte interno do MQTT nos SDKs do dispositivo IoT do Azure."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eab70c1aa9c49a137c2ac1012449d57915fb0d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a><span data-ttu-id="3f7a2-104">Comunicar com o hub IoT usando o protocolo MQTT</span><span class="sxs-lookup"><span data-stu-id="3f7a2-104">Communicate with your IoT hub using the MQTT protocol</span></span>

<span data-ttu-id="3f7a2-105">O Hub IoT permite que dispositivos se comuniquem com os pontos de extremidade do dispositivo do Hub IoT usando o protocolo [MQTT v3.1.1][lnk-mqtt-org] na porta 8883 ou MQTT v3.1.1 sobre protocolo WebSocket na porta 443.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="3f7a2-106">Hub IoT exige que todas as comunicações de dispositivo a sejam protegidas usando o TLS/SSL (portanto, Hub IoT não oferece suporte a conexões não seguras pela porta 1883).</span><span class="sxs-lookup"><span data-stu-id="3f7a2-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-to-iot-hub"></a><span data-ttu-id="3f7a2-107">Conectando-se ao Hub IoT</span><span class="sxs-lookup"><span data-stu-id="3f7a2-107">Connecting to IoT Hub</span></span>

<span data-ttu-id="3f7a2-108">Um dispositivo pode usar o protocolo MQTT para se conectar a um hub IoT usando as bibliotecas de [SDKs do IoT do Azure][lnk-device-sdks] ou usando o protocolo MQTT diretamente.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span></span>

## <a name="using-the-device-sdks"></a><span data-ttu-id="3f7a2-109">Usando os SDKs de dispositivo</span><span class="sxs-lookup"><span data-stu-id="3f7a2-109">Using the device SDKs</span></span>

<span data-ttu-id="3f7a2-110">Os [SDKs do cliente do dispositivo][lnk-device-sdks] que são compatíveis com o protocolo MQTT estão disponíveis para Java, Node.js, C, C# e Python.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="3f7a2-111">Os SDKs do dispositivo usam a cadeia de conexão do Hub IoT padrão para estabelecer uma conexão com um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span></span> <span data-ttu-id="3f7a2-112">Para usar o protocolo MQTT, o parâmetro do protocolo do cliente deve ser definido como **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span></span> <span data-ttu-id="3f7a2-113">Por padrão, os SDKs do dispositivo se conectam a um Hub IoT com o sinalizador **CleanSession** definido como **0** e usam **QoS 1** para troca de mensagens com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span></span>

<span data-ttu-id="3f7a2-114">Quando um dispositivo é conectado a um Hub IoT, os SDKs do dispositivo fornecem métodos que permitem que o dispositivo envie mensagens para um Hub IoT e receba mensagens dele.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span></span>

<span data-ttu-id="3f7a2-115">A tabela a seguir contém links para exemplos de código de cada linguagem compatível e especifica o parâmetro a ser usado para estabelecer uma conexão com o Hub IoT usando o protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span></span>

| <span data-ttu-id="3f7a2-116">Linguagem</span><span class="sxs-lookup"><span data-stu-id="3f7a2-116">Language</span></span> | <span data-ttu-id="3f7a2-117">Parâmetro do protocolo</span><span class="sxs-lookup"><span data-stu-id="3f7a2-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="3f7a2-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="3f7a2-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="3f7a2-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="3f7a2-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="3f7a2-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="3f7a2-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="3f7a2-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="3f7a2-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="3f7a2-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="3f7a2-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="3f7a2-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="3f7a2-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="3f7a2-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="3f7a2-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="3f7a2-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a><span data-ttu-id="3f7a2-128">Migrando um aplicativo de dispositivo de AMQP para MQTT</span><span class="sxs-lookup"><span data-stu-id="3f7a2-128">Migrating a device app from AMQP to MQTT</span></span>

<span data-ttu-id="3f7a2-129">Se você estiver usando o [SDKs de cliente de dispositivo][lnk-device-sdks], a mudança do uso de AMQP para MQTT exige alteração do parâmetro de protocolo na inicialização do cliente, conforme mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated previously.</span></span>

<span data-ttu-id="3f7a2-130">Ao fazer isso, verifique os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-130">When doing so, make sure to check the following items:</span></span>

* <span data-ttu-id="3f7a2-131">AMQP retorna erros para várias condições, enquanto MQTT encerra a conexão.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span></span> <span data-ttu-id="3f7a2-132">Como resultado, sua lógica de manipulação de exceções pode exigir algumas alterações.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="3f7a2-133">MQTT não dá suporte a operações de *rejeição* quando recebe [mensagens da nuvem para do dispositivo][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="3f7a2-134">Se seu aplicativo de back-end precisar receber uma resposta do aplicativo do dispositivo, considere usar [métodos diretos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-the-mqtt-protocol-directly"></a><span data-ttu-id="3f7a2-135">Usando o protocolo MQTT diretamente</span><span class="sxs-lookup"><span data-stu-id="3f7a2-135">Using the MQTT protocol directly</span></span>
<span data-ttu-id="3f7a2-136">Se um dispositivo não puder usar os SDKs do dispositivo, ele poderá se conectar com os pontos de extremidade públicos do dispositivo usando o protocolo MQTT na porta 8883.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol on port 8883.</span></span> <span data-ttu-id="3f7a2-137">No pacote **CONNECT** , o dispositivo deve usar os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-137">In the **CONNECT** packet the device should use the following values:</span></span>

* <span data-ttu-id="3f7a2-138">No campo **ClientId**, use o **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-138">For the **ClientId** field, use the **deviceId**.</span></span>
* <span data-ttu-id="3f7a2-139">No campo **Username**, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, em que {iothubhostname} é o CName completo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span></span>

    <span data-ttu-id="3f7a2-140">Por exemplo, se o nome de seu Hub IoT for **contoso.azure-devices.net** e se o nome do dispositivo for **MyDevice01**, o campo **Username** completo deverá conter `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="3f7a2-141">No campo **Senha** use um token SAS.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-141">For the **Password** field, use a SAS token.</span></span> <span data-ttu-id="3f7a2-142">O formato do token SAS é o mesmo, conforme descrito para os protocolos HTTP e AMQP:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="3f7a2-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="3f7a2-144">Para saber mais sobre como gerar tokens SAS, confira a seção de dispositivo de [Usar tokens de segurança do Hub IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="3f7a2-145">Durante o teste, você também pode usar a ferramenta [gerenciador de dispositivo][lnk-device-explorer] para gerar rapidamente um token SAS que pode ser copiado e colado em seu próprio código:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="3f7a2-146">Acesse a guia **Gerenciamento** no **Gerenciador de Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-146">Go to the **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="3f7a2-147">Clique em **Token SAS** (parte superior direita).</span><span class="sxs-lookup"><span data-stu-id="3f7a2-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="3f7a2-148">Em **SASTokenForm**, selecione seu dispositivo no menu suspenso **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span></span> <span data-ttu-id="3f7a2-149">Defina o **TTL**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="3f7a2-150">Clique em **Gerar** para criar o token.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-150">Click **Generate** to create your token.</span></span>

     <span data-ttu-id="3f7a2-151">O token SAS gerado tem esta estrutura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="3f7a2-152">A parte disso que deve ser usada, como no campo **Senha**, para se conectar usando MQTT é: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="3f7a2-153">Para pacotes de conexão e desconexão do MQTT, o Hub IoT emite um evento no canal **Monitoramento de operações** com informações adicionais que podem ajudar você a solucionar problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="3f7a2-154">Enviando mensagens de dispositivo para nuvem</span><span class="sxs-lookup"><span data-stu-id="3f7a2-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="3f7a2-155">Depois de fazer uma conexão bem-sucedida, um dispositivo pode enviar mensagens ao IoT Hub usando `devices/{device_id}/messages/events/` ou `devices/{device_id}/messages/events/{property_bag}` como um **nome de tópico**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="3f7a2-156">O elemento `{property_bag}` habilita o dispositivo a enviar mensagens com propriedades adicionais em um formato codificado de URL.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="3f7a2-157">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="3f7a2-158">Esse elemento `{property_bag}` usa a mesma codificação para cadeias de caracteres de consulta do protocolo HTTP.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span></span>
>
>

<span data-ttu-id="3f7a2-159">O aplicativo do dispositivo também pode usar `devices/{device_id}/messages/events/{property_bag}` como o **nome do tópico Will** para definir *mensagens Will* a serem encaminhadas como uma mensagem de telemetria.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span></span>

- <span data-ttu-id="3f7a2-160">O Hub IoT não dá suporte a mensagens de QoS 2.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="3f7a2-161">Se um aplicativo de dispositivo publicar uma mensagem com o **QoS 2**, o Hub IoT fechará a conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span></span>
- <span data-ttu-id="3f7a2-162">O Hub IoT não persiste mensagens de retenção.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="3f7a2-163">Se um dispositivo envia uma mensagem com o sinalizador **RETAIN** definido como 1, o Hub IoT adiciona a propriedade de aplicativo **x-opt-retain** à mensagem.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span></span> <span data-ttu-id="3f7a2-164">Nesse caso, em vez de persistir a mensagem de retenção, o Hub IoT a transmite ao aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span></span>
- <span data-ttu-id="3f7a2-165">O Hub IoT oferece suporte apenas a uma conexão MQTT ativa por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="3f7a2-166">Qualquer nova conexão MQTT em nome da mesma ID de dispositivo faz com que o Hub IoT descarte a conexão existente.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span></span>

<span data-ttu-id="3f7a2-167">Para obter mais informações, consulte [Guia do desenvolvedor do sistema de mensagens][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="3f7a2-168">Recebendo mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="3f7a2-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="3f7a2-169">Para receber mensagens do Hub IoT, um dispositivo deve fazer uma assinatura usando `devices/{device_id}/messages/devicebound/#` como um **Filtro do Tópico**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="3f7a2-170">O curinga de vários níveis **#** no filtro de tópico é usado apenas para permitir que o dispositivo receba propriedades adicionais no nome do tópico.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span></span> <span data-ttu-id="3f7a2-171">O Hub IoT não permite o uso de caracteres curinga **#** ou **?**</span><span class="sxs-lookup"><span data-stu-id="3f7a2-171">IoT Hub does not allow the usage of the **#** or **?**</span></span> <span data-ttu-id="3f7a2-172">para filtragem de subtópicos.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="3f7a2-173">Como o Hub IoT Hub não é um agente de mensagens pub-sub de finalidade geral, ele suporta apenas os nomes de tópico e filtros de tópico documentados.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span></span>

<span data-ttu-id="3f7a2-174">O dispositivo só receberá mensagens do Hub IoT depois de assinar com êxito o ponto de extremidade específico ao dispositivo, representado pelo filtro de tópico `devices/{device_id}/messages/devicebound/#`.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-174">The device does not receive any messages from IoT Hub, until it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="3f7a2-175">Depois que a assinatura tiver sido estabelecida com êxito, o dispositivo começa a receber apenas as mensagens de nuvem para dispositivos que foram enviadas para ele após o momento da assinatura.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-175">After successful subscription has been established, the device starts receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span></span> <span data-ttu-id="3f7a2-176">Se o dispositivo se conectar com o sinalizador **CleanSession** definido como **0**, a assinatura será persistida entre as diferentes sessões.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-176">If the device connects with **CleanSession** flag set to **0**, the subscription is persisted across different sessions.</span></span> <span data-ttu-id="3f7a2-177">Nesse caso, na próxima vez que ele se conectar com **CleanSession 0**, o dispositivo receberá mensagens pendentes que foram enviadas a ele enquanto ele estava desconectado.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-177">In this case, the next time it connects with **CleanSession 0** the device receives outstanding messages that have been sent to it while it was disconnected.</span></span> <span data-ttu-id="3f7a2-178">Se o dispositivo usar o sinalizador **CleanSession** definido como **1**, não receberá todas as mensagens do Hub IoT até que ele se inscreva no ponto de extremidade do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-178">If the device uses **CleanSession** flag set to **1** though, it does not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span></span>

<span data-ttu-id="3f7a2-179">IoT Hub entrega mensagens com o **Nome do Tópico** `devices/{device_id}/messages/devicebound/` ou `devices/{device_id}/messages/devicebound/{property_bag}` se houver propriedades de mensagem.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="3f7a2-180">`{property_bag}` contém pares de chave/valor codificados de URL das propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="3f7a2-181">Somente propriedades de aplicativo e propriedades do sistema definível pelo usuário (como **messageId** ou **correlationId**) estão incluídas no recipiente de propriedades.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span></span> <span data-ttu-id="3f7a2-182">Os nomes de propriedade do sistema têm o prefixo **$**; as propriedades de aplicativo usam o nome da propriedade original sem prefixo.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span></span>

<span data-ttu-id="3f7a2-183">Quando um aplicativo do dispositivo assina um tópico com o **QoS 2**, o Hub IoT concede, no máximo, o nível 1 do QoS no pacote **SUBACK**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span></span> <span data-ttu-id="3f7a2-184">Depois disso, o Hub IoT entrega mensagens ao dispositivo usando QoS 1.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-184">After that, IoT Hub delivers messages to the device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="3f7a2-185">Recuperando as propriedades de um dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="3f7a2-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="3f7a2-186">Primeiro, um dispositivo assina `$iothub/twin/res/#` para receber respostas da operação.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span></span> <span data-ttu-id="3f7a2-187">Em seguida, ele envia uma mensagem vazia ao tópico `$iothub/twin/GET/?$rid={request id}`, com um valor preenchido como a **ID da solicitação**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**.</span></span> <span data-ttu-id="3f7a2-188">O serviço então envia uma mensagem de resposta que contém os dados do dispositivo gêmeo no tópico `$iothub/twin/res/{status}/?$rid={request id}`, usando a mesma **ID de solicitação** da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-188">The service then sends a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span></span>

<span data-ttu-id="3f7a2-189">A ID da solicitação pode ser qualquer valor válido de um valor da propriedade de mensagem, de acordo com o [Guia do desenvolvedor do sistema de mensagens do Hub IoT][lnk-messaging] e o status é validado como um inteiro.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-189">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="3f7a2-190">O corpo da resposta contém a seção Propriedades do dispositivo gêmeo:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-190">The response body contains the properties section of the device twin:</span></span>

<span data-ttu-id="3f7a2-191">O corpo da entrada do Registro de identidade limitado ao membro “propriedades”, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-191">The body of the identity registry entry limited to the “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="3f7a2-192">Os códigos de status possíveis são:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-192">The possible status codes are:</span></span>

|<span data-ttu-id="3f7a2-193">Status</span><span class="sxs-lookup"><span data-stu-id="3f7a2-193">Status</span></span> | <span data-ttu-id="3f7a2-194">Descrição</span><span class="sxs-lookup"><span data-stu-id="3f7a2-194">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="3f7a2-195">200</span><span class="sxs-lookup"><span data-stu-id="3f7a2-195">200</span></span> | <span data-ttu-id="3f7a2-196">Sucesso</span><span class="sxs-lookup"><span data-stu-id="3f7a2-196">Success</span></span> |
| <span data-ttu-id="3f7a2-197">429</span><span class="sxs-lookup"><span data-stu-id="3f7a2-197">429</span></span> | <span data-ttu-id="3f7a2-198">Número excessivo de solicitações (limitado), de acordo com a [Limitação do Hub IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-198">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="3f7a2-199">5**</span><span class="sxs-lookup"><span data-stu-id="3f7a2-199">5**</span></span> | <span data-ttu-id="3f7a2-200">Erros do servidor</span><span class="sxs-lookup"><span data-stu-id="3f7a2-200">Server errors</span></span> |

<span data-ttu-id="3f7a2-201">Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-201">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="3f7a2-202">Atualizar as propriedades relatadas do dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="3f7a2-202">Update device twin's reported properties</span></span>

<span data-ttu-id="3f7a2-203">A sequência a seguir descreve como um dispositivo atualiza as propriedades relatadas no dispositivo gêmeo no Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-203">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span></span>

1. <span data-ttu-id="3f7a2-204">Primeiro, um dispositivo deve assinar o tópico `$iothub/twin/res/#` para receber respostas da operação do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-204">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="3f7a2-205">Um dispositivo envia uma mensagem que contém a atualização do dispositivo gêmeo para o tópico `$iothub/twin/PATCH/properties/reported/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-205">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="3f7a2-206">Essa mensagem inclui um valor de **id da solicitação**.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-206">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="3f7a2-207">Em seguida, o serviço envia uma mensagem de resposta que contém o novo valor de ETag para a coleção de propriedades relatadas no tópico `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-207">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="3f7a2-208">Essa mensagem de resposta usa a mesma **id de solicitação** da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-208">This response message uses the same **request id** as the request.</span></span>

<span data-ttu-id="3f7a2-209">O corpo da mensagem de solicitação contém um documento JSON, que fornece novos valores para as propriedades relatadas (nenhuma outra propriedade ou metadados podem ser modificados).</span><span class="sxs-lookup"><span data-stu-id="3f7a2-209">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="3f7a2-210">Cada membro no documento JSON atualiza ou adiciona o membro correspondente no documento do dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-210">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span></span> <span data-ttu-id="3f7a2-211">Um membro definido como `null` exclui o membro do objeto recipiente.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-211">A member set to `null`, deletes the member from the containing object.</span></span> <span data-ttu-id="3f7a2-212">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-212">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="3f7a2-213">Os códigos de status possíveis são:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-213">The possible status codes are:</span></span>

|<span data-ttu-id="3f7a2-214">Status</span><span class="sxs-lookup"><span data-stu-id="3f7a2-214">Status</span></span> | <span data-ttu-id="3f7a2-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="3f7a2-215">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="3f7a2-216">200</span><span class="sxs-lookup"><span data-stu-id="3f7a2-216">200</span></span> | <span data-ttu-id="3f7a2-217">Sucesso</span><span class="sxs-lookup"><span data-stu-id="3f7a2-217">Success</span></span> |
| <span data-ttu-id="3f7a2-218">400</span><span class="sxs-lookup"><span data-stu-id="3f7a2-218">400</span></span> | <span data-ttu-id="3f7a2-219">Solicitação inválida.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-219">Bad Request.</span></span> <span data-ttu-id="3f7a2-220">JSON malformado</span><span class="sxs-lookup"><span data-stu-id="3f7a2-220">Malformed JSON</span></span> |
| <span data-ttu-id="3f7a2-221">429</span><span class="sxs-lookup"><span data-stu-id="3f7a2-221">429</span></span> | <span data-ttu-id="3f7a2-222">Número excessivo de solicitações (limitado), de acordo com a [Limitação do Hub IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-222">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="3f7a2-223">5**</span><span class="sxs-lookup"><span data-stu-id="3f7a2-223">5**</span></span> | <span data-ttu-id="3f7a2-224">Erros do servidor</span><span class="sxs-lookup"><span data-stu-id="3f7a2-224">Server errors</span></span> |

<span data-ttu-id="3f7a2-225">Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-225">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="3f7a2-226">Recebendo notificações de atualização de propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="3f7a2-226">Receiving desired properties update notifications</span></span>

<span data-ttu-id="3f7a2-227">Quando um dispositivo é conectado, o Hub IoT envia notificações para o tópico `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que contêm o conteúdo da atualização executada pelo back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-227">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span></span> <span data-ttu-id="3f7a2-228">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-228">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="3f7a2-229">Em relação às atualizações de propriedade, valores `null` significam que o membro do objeto JSON está sendo excluído.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-229">As for property updates, `null` values means that the JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="3f7a2-230">O Hub IoT gera notificações de alteração somente quando os dispositivos estão conectados.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-230">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="3f7a2-231">Lembre-se de implementar o [fluxo de reconexão do dispositivo][lnk-devguide-twin-reconnection] para manter as propriedades desejadas sincronizadas entre o Hub IoT e o aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-231">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span></span>

<span data-ttu-id="3f7a2-232">Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-232">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-to-a-direct-method"></a><span data-ttu-id="3f7a2-233">Responder a um método direto</span><span class="sxs-lookup"><span data-stu-id="3f7a2-233">Respond to a direct method</span></span>

<span data-ttu-id="3f7a2-234">Primeiro, um dispositivo precisa assinar `$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-234">First, a device has to subscribe to `$iothub/methods/POST/#`.</span></span> <span data-ttu-id="3f7a2-235">O Hub IoT envia solicitações de método para o tópico `$iothub/methods/POST/{method name}/?$rid={request id}` com um corpo vazio ou JSON válido.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-235">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="3f7a2-236">Para responder, o dispositivo envia uma mensagem com um corpo vazio ou um JSON válido para o tópico `$iothub/methods/res/{status}/?$rid={request id}`, onde a **ID da solicitação** tem que corresponder à que está na mensagem de solicitação, e o **status** deverá ser um número inteiro.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-236">To respond, the device sends a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span></span>

<span data-ttu-id="3f7a2-237">Para obter mais informações, consulte [Guia do desenvolvedor do método direto][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-237">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="3f7a2-238">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="3f7a2-238">Additional considerations</span></span>

<span data-ttu-id="3f7a2-239">Como uma consideração final, se você precisar personalizar o comportamento do protocolo MQTT no lado da nuvem, deverá examinar o [Gateway de protocolo IoT do Azure][lnk-azure-protocol-gateway], que permite que você implante um gateway de protocolo personalizado de alto desempenho que interage diretamente com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-239">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="3f7a2-240">O gateway do protocolo IoT do Azure permite que você personalize o protocolo de dispositivo para acomodar as implantações de MQTT de nível industrial ou outros protocolos personalizados.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-240">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="3f7a2-241">Essa abordagem exige, no entanto, que você execute e opere um gateway de protocolo personalizado.</span><span class="sxs-lookup"><span data-stu-id="3f7a2-241">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f7a2-242">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f7a2-242">Next steps</span></span>

<span data-ttu-id="3f7a2-243">Para saber mais sobre o protocolo MQTT, consulte a [documentação do MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="3f7a2-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="3f7a2-244">Para saber mais sobre como planejar sua implantação do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-244">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="3f7a2-245">[Catálogo de dispositivos Azure Certified para IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-245">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="3f7a2-246">[Suporte a protocolos adicionais][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-246">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="3f7a2-247">[Comparar com Hubs de Eventos][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-247">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="3f7a2-248">[Escala, alta disponibilidade e recuperação de desastre][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-248">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="3f7a2-249">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="3f7a2-249">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3f7a2-250">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-250">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3f7a2-251">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="3f7a2-251">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
