---
title: "Entender os métodos diretos do Hub IoT do Azure | Microsoft Docs"
description: "Guia de desenvolvedor – use métodos diretos para invocar código em seus dispositivos de um aplicativo de serviço."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="b03bf-103">Entender e chamar métodos diretos do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="b03bf-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="b03bf-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b03bf-104">Overview</span></span>
<span data-ttu-id="b03bf-105">O Hub IoT permite invocar métodos diretos em dispositivos da nuvem.</span><span class="sxs-lookup"><span data-stu-id="b03bf-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="b03bf-106">Os métodos diretos representam uma interação entre solicitação e resposta com um dispositivo semelhante a uma chamada HTTP, na qual eles são bem-sucedidos ou falham imediatamente (depois que o tempo limite especificado pelo usuário é atingido).</span><span class="sxs-lookup"><span data-stu-id="b03bf-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="b03bf-107">Isso é útil para cenários em que a ação imediata é diferente dependendo da capacidade de resposta do dispositivo, como enviar uma ativação por SMS para um dispositivo se o dispositivo está offline (com o SMS sendo mais caro do que uma chamada de método).</span><span class="sxs-lookup"><span data-stu-id="b03bf-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="b03bf-108">Cada método de dispositivo tem como alvo um único dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b03bf-108">Each device method targets a single device.</span></span> <span data-ttu-id="b03bf-109">Os [Trabalhos][lnk-devguide-jobs] são uma maneira de invocar métodos diretos em vários dispositivos e agendar invocação de método para dispositivos desconectados.</span><span class="sxs-lookup"><span data-stu-id="b03bf-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="b03bf-110">Qualquer pessoa com permissões de **conectar serviço** no Hub IoT pode invocar um método em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b03bf-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="b03bf-111">Quando usar</span><span class="sxs-lookup"><span data-stu-id="b03bf-111">When to use</span></span>
<span data-ttu-id="b03bf-112">Os métodos diretos seguem um padrão de solicitação e resposta e se destinam a comunicações que exigem confirmação imediata de seus resultados, normalmente controle interativo do dispositivo, por exemplo, ligar uma ventoinha.</span><span class="sxs-lookup"><span data-stu-id="b03bf-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="b03bf-113">Veja [Cloud-to-device communication guidance][lnk-c2d-guidance] (Diretrizes de comunicação da nuvem para o dispositivo) se estiver em dúvida entre o uso de propriedades desejadas, métodos diretos ou mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b03bf-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="b03bf-114">Ciclo de vida do método</span><span class="sxs-lookup"><span data-stu-id="b03bf-114">Method lifecycle</span></span>
<span data-ttu-id="b03bf-115">Os métodos diretos são implementados no dispositivo e podem precisar ou não de entradas no conteúdo do método para instanciar corretamente.</span><span class="sxs-lookup"><span data-stu-id="b03bf-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="b03bf-116">Você invoca um método direto por meio de um URI voltado para serviços (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="b03bf-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="b03bf-117">Um dispositivo recebe métodos diretos por meio de um tópico MQTT específico ao dispositivo (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="b03bf-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="b03bf-118">Podemos dar suporte a métodos diretos em mais protocolos de rede do lado do dispositivo no futuro.</span><span class="sxs-lookup"><span data-stu-id="b03bf-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="b03bf-119">Quando você invoca um método direto em um dispositivo, os valores e nomes de propriedade só podem conter caracteres alfanuméricos imprimíveis US-ASCII, exceto pelo seguinte conjunto: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="b03bf-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="b03bf-120">Os métodos diretos são síncronos e obtêm êxito ou falham após o tempo limite (padrão: 30 segundos, configurável para até 3.600 segundos).</span><span class="sxs-lookup"><span data-stu-id="b03bf-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="b03bf-121">Os métodos diretos são úteis em cenários interativos em que você deseja que um dispositivo atue somente, e somente se, o dispositivo estiver online e recebendo comandos, como acender uma luz usando um telefone.</span><span class="sxs-lookup"><span data-stu-id="b03bf-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="b03bf-122">Nesses cenários, você deseja ver uma falha ou êxito imediatamente, para que o serviço de nuvem possa atuar quanto ao resultado o mais rápido possível.</span><span class="sxs-lookup"><span data-stu-id="b03bf-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="b03bf-123">O dispositivo pode retornar algum corpo de mensagem como resultado do método, mas não é obrigatório que o método faça isso.</span><span class="sxs-lookup"><span data-stu-id="b03bf-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="b03bf-124">Não há nenhuma garantia quanto à ordenação ou semântica de simultaneidade nas chamadas de método.</span><span class="sxs-lookup"><span data-stu-id="b03bf-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="b03bf-125">O método direto serve somente para HTTP do lado da nuvem, e somente MQTT do lado do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b03bf-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="b03bf-126">A carga das solicitações e respostas do método é um documento JSON de até 8 KB.</span><span class="sxs-lookup"><span data-stu-id="b03bf-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="b03bf-127">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="b03bf-127">Reference topics:</span></span>
<span data-ttu-id="b03bf-128">Os tópicos de referência a seguir fornecem a você mais informações sobre como usar os métodos diretos.</span><span class="sxs-lookup"><span data-stu-id="b03bf-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="b03bf-129">Invocar um método direto de um aplicativo back-end</span><span class="sxs-lookup"><span data-stu-id="b03bf-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="b03bf-130">Invocação de método</span><span class="sxs-lookup"><span data-stu-id="b03bf-130">Method invocation</span></span>
<span data-ttu-id="b03bf-131">Invocações de método direto em um dispositivo são chamadas HTTP, que compreendem:</span><span class="sxs-lookup"><span data-stu-id="b03bf-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="b03bf-132">O *URI* específico para o dispositivo (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="b03bf-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="b03bf-133">A *método* POST</span><span class="sxs-lookup"><span data-stu-id="b03bf-133">The POST *method*</span></span>
* <span data-ttu-id="b03bf-134">*Cabeçalhos* que contêm a autorização, ID da solicitação, tipo de conteúdo e codificação de conteúdo</span><span class="sxs-lookup"><span data-stu-id="b03bf-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="b03bf-135">Um *corpo* JSON transparente no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="b03bf-135">A transparent JSON *body* in the following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="b03bf-136">Tempo limite em segundos.</span><span class="sxs-lookup"><span data-stu-id="b03bf-136">Timeout is in seconds.</span></span> <span data-ttu-id="b03bf-137">Se o tempo limite não tiver sido definido, o padrão será 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="b03bf-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="b03bf-138">Resposta</span><span class="sxs-lookup"><span data-stu-id="b03bf-138">Response</span></span>
<span data-ttu-id="b03bf-139">O aplicativo de back-end recebe uma resposta que inclui:</span><span class="sxs-lookup"><span data-stu-id="b03bf-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="b03bf-140">*Código de status HTTP*, que é usado para erros provenientes do Hub IoT, incluindo um erro 404 para dispositivos que não estão conectados</span><span class="sxs-lookup"><span data-stu-id="b03bf-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="b03bf-141">*Cabeçalhos* que contêm a ETag, a ID de solicitação, tipo de conteúdo e codificação de conteúdo</span><span class="sxs-lookup"><span data-stu-id="b03bf-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="b03bf-142">Um *corpo* JSON no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="b03bf-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="b03bf-143">`status` e `body` são fornecidos pelo dispositivo e usados para responder com o código de status e/ou descrição do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b03bf-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="b03bf-144">Tratar um método direto em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="b03bf-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="b03bf-145">Invocação de método</span><span class="sxs-lookup"><span data-stu-id="b03bf-145">Method invocation</span></span>
<span data-ttu-id="b03bf-146">Os dispositivos recebem solicitações de método direto sobre o tópico MQTT: `$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="b03bf-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="b03bf-147">O corpo que o dispositivo recebe está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="b03bf-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="b03bf-148">As solicitações de método são QoS 0.</span><span class="sxs-lookup"><span data-stu-id="b03bf-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="b03bf-149">Resposta</span><span class="sxs-lookup"><span data-stu-id="b03bf-149">Response</span></span>
<span data-ttu-id="b03bf-150">O dispositivo envia as respostas para `$iothub/methods/res/{status}/?$rid={request id}`, em que:</span><span class="sxs-lookup"><span data-stu-id="b03bf-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="b03bf-151">A propriedade `status` é o status de execução fornecido pelo dispositivo da execução do método.</span><span class="sxs-lookup"><span data-stu-id="b03bf-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="b03bf-152">A propriedade `$rid` é a ID de solicitação de invocação do método recebida do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b03bf-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="b03bf-153">O corpo é definido pelo dispositivo e pode ter qualquer status.</span><span class="sxs-lookup"><span data-stu-id="b03bf-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="b03bf-154">Material de referência adicional</span><span class="sxs-lookup"><span data-stu-id="b03bf-154">Additional reference material</span></span>
<span data-ttu-id="b03bf-155">Outros tópicos de referência no Guia do desenvolvedor do Hub IoT incluem:</span><span class="sxs-lookup"><span data-stu-id="b03bf-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="b03bf-156">[Pontos de extremidade do Hub IoT][lnk-endpoints] descreve os vários pontos de extremidade que cada Hub IoT expõe para operações de tempo de execução e de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="b03bf-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="b03bf-157">[Limitação e cotas][lnk-quotas] descreve as cotas que se aplicam ao serviço Hub IoT e o comportamento de limitação esperado ao usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b03bf-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="b03bf-158">[SDKs de dispositivo e serviço IoT do Azure][lnk-sdks] lista os vários SDKs de linguagem que você pode usar no desenvolvimento de aplicativos de dispositivo e de serviço que interagem com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b03bf-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="b03bf-159">[Linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens][lnk-query] descreve a linguagem de consulta do Hub IoT que você pode usar para recuperar informações do Hub IoT sobre dispositivos gêmeos e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="b03bf-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="b03bf-160">[Suporte ao MQTT do Hub IoT][lnk-devguide-mqtt] fornece mais informações sobre o suporte do Hub IoT para o protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="b03bf-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b03bf-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b03bf-161">Next steps</span></span>
<span data-ttu-id="b03bf-162">Agora que você aprendeu a usar métodos diretos, pode ser interessante ler o seguinte tópico do Guia do Desenvolvedor do Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="b03bf-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="b03bf-163">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="b03bf-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="b03bf-164">Se você quiser experimentar alguns dos conceitos descritos neste artigo, talvez se interesse pelo seguinte tutorial de Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="b03bf-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="b03bf-165">[Usar métodos diretos][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="b03bf-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
