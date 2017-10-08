---
title: aaaUnderstand suporte do Azure IoT Hub MQTT | Microsoft Docs
description: "Desenvolvedor guiá - suporte para dispositivos que se conectam tooan IoT Hub voltados para o dispositivo usando o ponto de extremidade Olá protocolo MQTT. Inclui informações sobre suporte interno ao MQTT Olá SDKs de dispositivo IoT do Azure."
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
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="3aba8-104">Se comunicar com o hub IoT usando o protocolo MQTT Olá</span><span class="sxs-lookup"><span data-stu-id="3aba8-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="3aba8-105">IoT Hub permite que dispositivos toocommunicate com hello Hub IoT dispositivo pontos de extremidade usando Olá [v MQTT 3.1.1] [ lnk-mqtt-org] protocolo porta 8883 ou v 3.1.1 MQTT com o protocolo WebSocket na porta 443.</span><span class="sxs-lookup"><span data-stu-id="3aba8-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="3aba8-106">IoT Hub requer que todos os toobe de comunicação do dispositivo protegida usando SSL/TLS (assim, IoT Hub não oferece suporte a conexões não seguras pela porta 1883).</span><span class="sxs-lookup"><span data-stu-id="3aba8-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="3aba8-107">Conectando tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="3aba8-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="3aba8-108">Um dispositivo pode usar hub de IoT Olá MQTT protocolo tooconnect tooan usando bibliotecas Olá Olá [SDKs do Azure IoT] [ lnk-device-sdks] ou usando o protocolo de MQTT saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="3aba8-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="3aba8-109">Usando o dispositivo Olá SDKs</span><span class="sxs-lookup"><span data-stu-id="3aba8-109">Using hello device SDKs</span></span>

<span data-ttu-id="3aba8-110">[Dispositivo SDKs] [ lnk-device-sdks] Olá que suporte o protocolo MQTT estão disponíveis para Java, Node.js, C, c# e Python.</span><span class="sxs-lookup"><span data-stu-id="3aba8-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="3aba8-111">usar o dispositivo de saudação SDKs saudação padrão cadeia de caracteres tooestablish um hub de IoT tooan conexão do IoT Hub conexão.</span><span class="sxs-lookup"><span data-stu-id="3aba8-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="3aba8-112">toouse Olá MQTT protocolo, parâmetro de protocolo de cliente hello deve ser definido muito**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="3aba8-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="3aba8-113">Por padrão, o dispositivo Olá SDKs conectar tooan IoT Hub com hello **CleanSession** sinalizador definido muito**0** e usar **QoS 1** para troca de mensagens com o hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="3aba8-114">Quando um dispositivo está conectado tooan hub IoT, dispositivo Olá SDKs forneça métodos que habilitar Olá dispositivo toosend mensagens tooand receber mensagens de um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3aba8-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="3aba8-115">Olá tabela a seguir contém links toocode exemplos para cada idioma suportado e especifica Olá parâmetro toouse tooestablish tooIoT uma conexão Hub usando o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="3aba8-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="3aba8-116">idioma</span><span class="sxs-lookup"><span data-stu-id="3aba8-116">Language</span></span> | <span data-ttu-id="3aba8-117">Parâmetro do protocolo</span><span class="sxs-lookup"><span data-stu-id="3aba8-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="3aba8-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="3aba8-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="3aba8-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="3aba8-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="3aba8-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="3aba8-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="3aba8-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="3aba8-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="3aba8-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="3aba8-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="3aba8-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="3aba8-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="3aba8-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="3aba8-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="3aba8-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="3aba8-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="3aba8-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="3aba8-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="3aba8-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="3aba8-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="3aba8-128">Migrando um aplicativo de dispositivo do AMQP tooMQTT</span><span class="sxs-lookup"><span data-stu-id="3aba8-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="3aba8-129">Se você estiver usando Olá [dispositivo SDKs][lnk-device-sdks], alternando de usar o AMQP tooMQTT requer a alteração do parâmetro de protocolo hello na inicialização do cliente hello como mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3aba8-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="3aba8-130">Ao fazer isso, certifique-se de saudação toocheck itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3aba8-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="3aba8-131">AMQP retorna erros para várias condições, enquanto MQTT encerra a conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="3aba8-132">Como resultado, sua lógica de manipulação de exceções pode exigir algumas alterações.</span><span class="sxs-lookup"><span data-stu-id="3aba8-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="3aba8-133">MQTT não oferece suporte a saudação *rejeitar* operações quando receber [mensagens de nuvem para dispositivo][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="3aba8-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="3aba8-134">Se seu aplicativo de back-end precisa tooreceive uma resposta do aplicativo para dispositivo hello, considere o uso de [direto métodos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="3aba8-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="3aba8-135">Usando o protocolo de MQTT saudação diretamente</span><span class="sxs-lookup"><span data-stu-id="3aba8-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="3aba8-136">Se um dispositivo não é possível usar o dispositivo Olá SDKs, ele ainda possa se conectar pontos de extremidade do dispositivo público toohello usando o protocolo de MQTT saudação na porta 8883.</span><span class="sxs-lookup"><span data-stu-id="3aba8-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="3aba8-137">Em Olá **conectar** dispositivo de saudação do pacote deve usar Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="3aba8-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="3aba8-138">Para Olá **ClientId** campo, use Olá **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="3aba8-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="3aba8-139">Para Olá **Username** campo, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, onde {iothubhostname} é Olá CName completa de hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="3aba8-140">Por exemplo, se hello nome do seu hub IoT é **contoso.azure devices.net** e se o nome de saudação do seu dispositivo é **MyDevice01**, Olá completo **Username** campo deve conter `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="3aba8-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="3aba8-141">Para Olá **senha** campo, use um token SAS.</span><span class="sxs-lookup"><span data-stu-id="3aba8-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="3aba8-142">formato de saudação do hello token SAS é Olá mesmo como para Olá HTTP e protocolos AMQP:</span><span class="sxs-lookup"><span data-stu-id="3aba8-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="3aba8-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="3aba8-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="3aba8-144">Para obter mais informações sobre como toogenerate tokens SAS, consulte a seção de dispositivo de saudação do [tokens de segurança usando IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="3aba8-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="3aba8-145">Durante o teste, você também pode usar o hello [explorer dispositivo] [ lnk-device-explorer] tooquickly ferramenta gerar um token SAS que você pode copiar e colar no seu próprio código:</span><span class="sxs-lookup"><span data-stu-id="3aba8-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="3aba8-146">Vá toohello **gerenciamento** guia **Gerenciador de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="3aba8-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="3aba8-147">Clique em **Token SAS** (parte superior direita).</span><span class="sxs-lookup"><span data-stu-id="3aba8-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="3aba8-148">Em **SASTokenForm**, selecione o dispositivo em Olá **DeviceID** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="3aba8-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="3aba8-149">Defina o **TTL**.</span><span class="sxs-lookup"><span data-stu-id="3aba8-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="3aba8-150">Clique em **gerar** toocreate seu token.</span><span class="sxs-lookup"><span data-stu-id="3aba8-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="3aba8-151">token SAS que é gerado Hello tem esta estrutura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="3aba8-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="3aba8-152">Olá parte esse token toouse como Olá **senha** tooconnect campo usando MQTT é: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="3aba8-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="3aba8-153">Para MQTT se conectar e desconectar pacotes, IoT Hub emite um evento em Olá **operações de monitoramento** canal com informações adicionais que podem ajudá-lo tootroubleshoot problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="3aba8-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="3aba8-154">Enviando mensagens de dispositivo para nuvem</span><span class="sxs-lookup"><span data-stu-id="3aba8-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="3aba8-155">Depois de fazer uma conexão bem-sucedida, um dispositivo pode enviar mensagens tooIoT Hub usando `devices/{device_id}/messages/events/` ou `devices/{device_id}/messages/events/{property_bag}` como um **o nome do tópico**.</span><span class="sxs-lookup"><span data-stu-id="3aba8-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="3aba8-156">Olá `{property_bag}` elemento permite que mensagens de saudação toosend do dispositivo com propriedades adicionais em um formato codificado de url.</span><span class="sxs-lookup"><span data-stu-id="3aba8-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="3aba8-157">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3aba8-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="3aba8-158">Isso `{property_bag}` elemento usa Olá a mesma codificação que cadeias de caracteres de consulta no protocolo de saudação HTTP.</span><span class="sxs-lookup"><span data-stu-id="3aba8-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="3aba8-159">também pode usar o aplicativo de dispositivo Olá `devices/{device_id}/messages/events/{property_bag}` como Olá **será o nome do tópico** toodefine *será mensagens* toobe encaminhada como uma mensagem de telemetria.</span><span class="sxs-lookup"><span data-stu-id="3aba8-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="3aba8-160">O Hub IoT não dá suporte a mensagens de QoS 2.</span><span class="sxs-lookup"><span data-stu-id="3aba8-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="3aba8-161">Se um aplicativo de dispositivo publica uma mensagem com **QoS 2**, IoT Hub fecha a conexão de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="3aba8-162">O Hub IoT não persiste mensagens de retenção.</span><span class="sxs-lookup"><span data-stu-id="3aba8-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="3aba8-163">Se um dispositivo envia uma mensagem de saudação **RETER** sinalizador definido too1, IoT Hub adiciona Olá **x-opt-reter** mensagem de toohello de propriedade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3aba8-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="3aba8-164">Nesse caso, em vez da saudação persistente reter a mensagem, o IoT Hub transmite toohello aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="3aba8-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="3aba8-165">O Hub IoT oferece suporte apenas a uma conexão MQTT ativa por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3aba8-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="3aba8-166">Qualquer conexão MQTT novo em nome hello mesma ID de dispositivo faz com que o IoT Hub conexão existente do toodrop hello.</span><span class="sxs-lookup"><span data-stu-id="3aba8-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="3aba8-167">Para obter mais informações, consulte [Guia do desenvolvedor do sistema de mensagens][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="3aba8-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="3aba8-168">Recebendo mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="3aba8-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="3aba8-169">mensagens de tooreceive de IoT Hub, um dispositivo deve assinar usando `devices/{device_id}/messages/devicebound/#` como um **tópico filtro**.</span><span class="sxs-lookup"><span data-stu-id="3aba8-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="3aba8-170">Olá curinga multinível  **#**  Olá filtro de tópico é usado somente tooallow Olá propriedades adicionais do dispositivo tooreceive no nome do tópico hello.</span><span class="sxs-lookup"><span data-stu-id="3aba8-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="3aba8-171">IoT Hub não permite o uso de saudação do hello  **#**  ou **?**</span><span class="sxs-lookup"><span data-stu-id="3aba8-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="3aba8-172">para filtragem de subtópicos.</span><span class="sxs-lookup"><span data-stu-id="3aba8-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="3aba8-173">Como o IoT Hub não é um agente de mensagens geral pub-sub, suporta apenas nomes de tópico Olá documentado e filtros de tópico.</span><span class="sxs-lookup"><span data-stu-id="3aba8-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="3aba8-174">Hello dispositivo não recebe as mensagens de IoT Hub, até que ele tenha assinado com êxito ponto de extremidade específico do dispositivo de tooits, representado pelo Olá `devices/{device_id}/messages/devicebound/#` filtro de tópico.</span><span class="sxs-lookup"><span data-stu-id="3aba8-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="3aba8-175">Depois de assinatura bem-sucedida foi estabelecida, o dispositivo Olá começa a receber mensagens de somente de nuvem para dispositivo que foram enviadas tooit após o tempo de saudação de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="3aba8-176">Se o dispositivo de saudação se conecta com **CleanSession** sinalizador definido muito**0**, assinatura de saudação é persistente entre as diferentes sessões.</span><span class="sxs-lookup"><span data-stu-id="3aba8-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="3aba8-177">Olá nesse caso, a próxima vez que ele se conecta com **CleanSession 0** dispositivo Olá recebe mensagens pendentes que foram enviadas tooit enquanto estava desconectado.</span><span class="sxs-lookup"><span data-stu-id="3aba8-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="3aba8-178">Se o dispositivo Olá usa **CleanSession** sinalizador definido muito**1** , não recebe as mensagens de IoT Hub até que ele assina tooits ponto de extremidade do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3aba8-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="3aba8-179">IoT Hub entrega mensagens com hello **o nome do tópico** `devices/{device_id}/messages/devicebound/`, ou `devices/{device_id}/messages/devicebound/{property_bag}` se houver quaisquer propriedades de mensagem.</span><span class="sxs-lookup"><span data-stu-id="3aba8-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="3aba8-180">`{property_bag}` contém pares de chave/valor codificados de URL das propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="3aba8-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="3aba8-181">Apenas as propriedades de aplicativo e as propriedades do sistema definível pelo usuário (como **messageId** ou **correlationId**) são incluídos no conjunto de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="3aba8-182">Nomes de propriedade do sistema têm o prefixo de saudação  **$** , propriedades do aplicativo usam o nome da propriedade original Olá sem prefixo.</span><span class="sxs-lookup"><span data-stu-id="3aba8-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="3aba8-183">Quando um aplicativo de dispositivo assina tópico tooa com **QoS 2**, IoT Hub concede o nível máximo QoS 1 em Olá **SUBACK** pacote.</span><span class="sxs-lookup"><span data-stu-id="3aba8-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="3aba8-184">Depois disso, o IoT Hub oferece dispositivo toohello de mensagens usando a QoS 1.</span><span class="sxs-lookup"><span data-stu-id="3aba8-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="3aba8-185">Recuperando as propriedades de um dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="3aba8-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="3aba8-186">Primeiro, um dispositivo assina muito`$iothub/twin/res/#`, respostas da operação de saudação tooreceive.</span><span class="sxs-lookup"><span data-stu-id="3aba8-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="3aba8-187">Em seguida, ele envia uma mensagem vazia tootopic `$iothub/twin/GET/?$rid={request id}`, com um valor preenchido para **id da solicitação**. serviço hello, em seguida, envia uma mensagem de resposta que contém dados de duas dispositivo Olá no tópico `$iothub/twin/res/{status}/?$rid={request id}`, usando Olá mesmo  **id da solicitação** como solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="3aba8-188">A ID da solicitação pode ser qualquer valor válido de um valor da propriedade de mensagem, de acordo com o [Guia do desenvolvedor do sistema de mensagens do Hub IoT][lnk-messaging] e o status é validado como um inteiro.</span><span class="sxs-lookup"><span data-stu-id="3aba8-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="3aba8-189">corpo da resposta de Olá contém uma seção de propriedades de saudação do duas de dispositivo de saudação:</span><span class="sxs-lookup"><span data-stu-id="3aba8-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="3aba8-190">corpo de saudação da entrada de registro de identidade Olá limitado toohello membro de "propriedades", por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3aba8-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

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

<span data-ttu-id="3aba8-191">Olá códigos de status possíveis são:</span><span class="sxs-lookup"><span data-stu-id="3aba8-191">hello possible status codes are:</span></span>

|<span data-ttu-id="3aba8-192">Status</span><span class="sxs-lookup"><span data-stu-id="3aba8-192">Status</span></span> | <span data-ttu-id="3aba8-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="3aba8-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="3aba8-194">200</span><span class="sxs-lookup"><span data-stu-id="3aba8-194">200</span></span> | <span data-ttu-id="3aba8-195">Sucesso</span><span class="sxs-lookup"><span data-stu-id="3aba8-195">Success</span></span> |
| <span data-ttu-id="3aba8-196">429</span><span class="sxs-lookup"><span data-stu-id="3aba8-196">429</span></span> | <span data-ttu-id="3aba8-197">Número excessivo de solicitações (limitado), de acordo com a [Limitação do Hub IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="3aba8-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="3aba8-198">5**</span><span class="sxs-lookup"><span data-stu-id="3aba8-198">5**</span></span> | <span data-ttu-id="3aba8-199">Erros do servidor</span><span class="sxs-lookup"><span data-stu-id="3aba8-199">Server errors</span></span> |

<span data-ttu-id="3aba8-200">Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="3aba8-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="3aba8-201">Atualizar as propriedades relatadas do dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="3aba8-201">Update device twin's reported properties</span></span>

<span data-ttu-id="3aba8-202">Olá sequência a seguir descreve como um dispositivo atualiza Olá relatado propriedades em duas de dispositivo Olá no IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="3aba8-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="3aba8-203">Um dispositivo deve se inscrever inicialmente toohello `$iothub/twin/res/#` respostas da operação do tópico tooreceive saudação do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3aba8-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="3aba8-204">Um dispositivo envia uma mensagem que contém a saudação dispositivo duas atualização toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` tópico.</span><span class="sxs-lookup"><span data-stu-id="3aba8-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="3aba8-205">Essa mensagem inclui um valor de **id da solicitação**.</span><span class="sxs-lookup"><span data-stu-id="3aba8-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="3aba8-206">Olá serviço, em seguida, envia uma mensagem de resposta que contém Olá novo valor de ETag para Olá a coleção de propriedades relatado no tópico `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="3aba8-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="3aba8-207">Essa mensagem de resposta usa Olá mesmo **id da solicitação** como solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="3aba8-208">Olá corpo da mensagem de solicitação contém um documento JSON, que fornece novos valores para as propriedades relatadas (podem ser modificado sem propriedades ou metadados).</span><span class="sxs-lookup"><span data-stu-id="3aba8-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="3aba8-209">Cada membro no documento JSON Olá atualizações ou Adicionar membro correspondente Olá no documento do duas do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="3aba8-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="3aba8-210">Um membro definido muito`null`, exclusões Olá membro de saudação que contém o objeto.</span><span class="sxs-lookup"><span data-stu-id="3aba8-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="3aba8-211">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3aba8-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="3aba8-212">Olá códigos de status possíveis são:</span><span class="sxs-lookup"><span data-stu-id="3aba8-212">hello possible status codes are:</span></span>

|<span data-ttu-id="3aba8-213">Status</span><span class="sxs-lookup"><span data-stu-id="3aba8-213">Status</span></span> | <span data-ttu-id="3aba8-214">Descrição</span><span class="sxs-lookup"><span data-stu-id="3aba8-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="3aba8-215">200</span><span class="sxs-lookup"><span data-stu-id="3aba8-215">200</span></span> | <span data-ttu-id="3aba8-216">Sucesso</span><span class="sxs-lookup"><span data-stu-id="3aba8-216">Success</span></span> |
| <span data-ttu-id="3aba8-217">400</span><span class="sxs-lookup"><span data-stu-id="3aba8-217">400</span></span> | <span data-ttu-id="3aba8-218">Solicitação inválida.</span><span class="sxs-lookup"><span data-stu-id="3aba8-218">Bad Request.</span></span> <span data-ttu-id="3aba8-219">JSON malformado</span><span class="sxs-lookup"><span data-stu-id="3aba8-219">Malformed JSON</span></span> |
| <span data-ttu-id="3aba8-220">429</span><span class="sxs-lookup"><span data-stu-id="3aba8-220">429</span></span> | <span data-ttu-id="3aba8-221">Número excessivo de solicitações (limitado), de acordo com a [Limitação do Hub IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="3aba8-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="3aba8-222">5**</span><span class="sxs-lookup"><span data-stu-id="3aba8-222">5**</span></span> | <span data-ttu-id="3aba8-223">Erros do servidor</span><span class="sxs-lookup"><span data-stu-id="3aba8-223">Server errors</span></span> |

<span data-ttu-id="3aba8-224">Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="3aba8-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="3aba8-225">Recebendo notificações de atualização de propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="3aba8-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="3aba8-226">Quando um dispositivo estiver conectado, o IoT Hub envia o tópico de toohello notificações `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que contêm o conteúdo de Olá Olá atualização executada pelo back-end de solução hello.</span><span class="sxs-lookup"><span data-stu-id="3aba8-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="3aba8-227">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3aba8-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="3aba8-228">Para atualizações de propriedade `null` valores significa que Olá JSON do objeto membro está sendo excluído.</span><span class="sxs-lookup"><span data-stu-id="3aba8-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="3aba8-229">O Hub IoT gera notificações de alteração somente quando os dispositivos estão conectados.</span><span class="sxs-lookup"><span data-stu-id="3aba8-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="3aba8-230">Verifique se Olá de tooimplement [fluxo de reconexão do dispositivo] [ lnk-devguide-twin-reconnection] tookeep Olá desejado propriedades sincronizadas entre o IoT Hub e o aplicativo de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3aba8-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="3aba8-231">Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="3aba8-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="3aba8-232">Método direto tooa de responder</span><span class="sxs-lookup"><span data-stu-id="3aba8-232">Respond tooa direct method</span></span>

<span data-ttu-id="3aba8-233">Primeiro, um dispositivo tem toosubscribe muito`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="3aba8-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="3aba8-234">IoT Hub envia o tópico do método solicitações toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, com um corpo vazio ou JSON válido.</span><span class="sxs-lookup"><span data-stu-id="3aba8-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="3aba8-235">toorespond, dispositivo Olá envia uma mensagem com um JSON válido ou um tópico do corpo vazio toohello `$iothub/methods/res/{status}/?$rid={request id}`, onde **id da solicitação** tem toomatch Olá um na mensagem de solicitação de saudação e **status** tem toobe um número inteiro .</span><span class="sxs-lookup"><span data-stu-id="3aba8-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="3aba8-236">Para obter mais informações, consulte [Guia do desenvolvedor do método direto][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="3aba8-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="3aba8-237">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="3aba8-237">Additional considerations</span></span>

<span data-ttu-id="3aba8-238">Como uma consideração final, se você precisar de comportamento de protocolo MQTT toocustomize Olá no lado de nuvem hello, você deve revisar Olá [gateway de protocolo do Azure IoT] [ lnk-azure-protocol-gateway] que permite a você toodeploy de alto desempenho gateway de protocolo personalizado que interage diretamente com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3aba8-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="3aba8-239">gateway do protocolo Hello IoT do Azure permite que você toocustomize Olá protocolo tooaccommodate brownfield MQTT implantações de dispositivos ou outros protocolos personalizados.</span><span class="sxs-lookup"><span data-stu-id="3aba8-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="3aba8-240">Essa abordagem exige, no entanto, que você execute e opere um gateway de protocolo personalizado.</span><span class="sxs-lookup"><span data-stu-id="3aba8-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aba8-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3aba8-241">Next steps</span></span>

<span data-ttu-id="3aba8-242">toolearn mais sobre o protocolo MQTT hello, consulte Olá [documentação MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="3aba8-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="3aba8-243">toolearn mais sobre como planejar sua implantação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="3aba8-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="3aba8-244">[Catálogo de dispositivos Azure Certified para IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="3aba8-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="3aba8-245">[Suporte a protocolos adicionais][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="3aba8-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="3aba8-246">[Comparar com Hubs de Eventos][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="3aba8-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="3aba8-247">[Escala, alta disponibilidade e recuperação de desastre][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="3aba8-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="3aba8-248">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="3aba8-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3aba8-249">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3aba8-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3aba8-250">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="3aba8-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
