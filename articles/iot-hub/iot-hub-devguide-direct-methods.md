---
title: "métodos de direcionar aaaUnderstand Azure IoT Hub | Microsoft Docs"
description: "Guia do desenvolvedor - use métodos diretos tooinvoke código em seus dispositivos de um aplicativo de serviço."
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
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="abea3-103">Entender e chamar métodos diretos do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="abea3-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="abea3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="abea3-104">Overview</span></span>
<span data-ttu-id="abea3-105">IoT Hub oferece métodos diretos de tooinvoke de capacidade nos dispositivos da nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="abea3-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="abea3-106">Métodos diretos representam uma interação de solicitação-resposta com um tooan semelhante dispositivo HTTP chamadas em que elas foram bem-sucedidas ou falham imediatamente (após um tempo limite especificado pelo usuário).</span><span class="sxs-lookup"><span data-stu-id="abea3-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="abea3-107">Isso é útil para cenários onde Olá ação imediata é diferente dependendo se o dispositivo de saudação foi capaz de toorespond, como o envio de um dispositivo do SMS wake-up tooa se um dispositivo estiver offline (sendo mais caro do que uma chamada de método SMS).</span><span class="sxs-lookup"><span data-stu-id="abea3-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="abea3-108">Cada método de dispositivo tem como alvo um único dispositivo.</span><span class="sxs-lookup"><span data-stu-id="abea3-108">Each device method targets a single device.</span></span> <span data-ttu-id="abea3-109">[Trabalhos] [ lnk-devguide-jobs] fornecem uma maneira tooinvoke métodos diretos em vários dispositivos e agendar a invocação de método para dispositivos desconectados.</span><span class="sxs-lookup"><span data-stu-id="abea3-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="abea3-110">Qualquer pessoa com permissões de **conectar serviço** no Hub IoT pode invocar um método em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="abea3-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="abea3-111">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="abea3-111">When toouse</span></span>
<span data-ttu-id="abea3-112">Métodos diretos seguem um padrão de solicitação-resposta e destinam-se para as comunicações que exigem a confirmação imediata de seus resultados, controle geralmente interativo do dispositivo hello, por exemplo tooturn em um ventilador.</span><span class="sxs-lookup"><span data-stu-id="abea3-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="abea3-113">Consulte também[orientação de comunicação de nuvem para dispositivo] [ lnk-c2d-guidance] em caso de dúvida, entre usando as propriedades desejadas, direcionar métodos ou mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="abea3-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="abea3-114">Ciclo de vida do método</span><span class="sxs-lookup"><span data-stu-id="abea3-114">Method lifecycle</span></span>
<span data-ttu-id="abea3-115">Métodos diretos são implementados no dispositivo hello e podem exigir a zero ou mais entradas no toocorrectly de carga do método hello instanciar.</span><span class="sxs-lookup"><span data-stu-id="abea3-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="abea3-116">Você invoca um método direto por meio de um URI voltado para serviços (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="abea3-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="abea3-117">Um dispositivo recebe métodos diretos por meio de um tópico MQTT específico ao dispositivo (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="abea3-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="abea3-118">Podemos pode oferecer suporte a métodos diretos em protocolos de rede de lado do dispositivo adicionais no futuro de saudação.</span><span class="sxs-lookup"><span data-stu-id="abea3-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="abea3-119">Quando você invoca um método em um dispositivo, valores e nomes de propriedade só podem conter US-ASCII imprimível alfanumérico, exceto qualquer em Olá conjunto a seguir: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="abea3-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="abea3-120">Direcionar métodos são síncronos e o êxito ou falha após o período de tempo limite da saudação (padrão: 30 segundos, definível pelo backup too3600 segundos).</span><span class="sxs-lookup"><span data-stu-id="abea3-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="abea3-121">Métodos diretos são úteis em cenários interativos onde deseja que um dispositivo tooact se e somente se o dispositivo de hello está online e recebendo comandos, como ativar a luz de um telefone.</span><span class="sxs-lookup"><span data-stu-id="abea3-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="abea3-122">Nesses cenários, você deseja toosee uma falha ou sucesso imediato para que serviço de nuvem Olá possa agir no resultado de saudação assim que possível.</span><span class="sxs-lookup"><span data-stu-id="abea3-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="abea3-123">dispositivo Olá pode retornar alguns corpo da mensagem como resultado do método hello, mas ele não é necessário para Olá método toodo para.</span><span class="sxs-lookup"><span data-stu-id="abea3-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="abea3-124">Não há nenhuma garantia quanto à ordenação ou semântica de simultaneidade nas chamadas de método.</span><span class="sxs-lookup"><span data-stu-id="abea3-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="abea3-125">Método direto são somente para HTTP do lado de nuvem hello e somente MQTT do lado do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="abea3-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="abea3-126">carga de saudação para método solicitações e respostas é um documento JSON para cima too8KB.</span><span class="sxs-lookup"><span data-stu-id="abea3-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="abea3-127">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="abea3-127">Reference topics:</span></span>
<span data-ttu-id="abea3-128">Olá seguintes tópicos de referência fornecem mais informações sobre como usar métodos diretos.</span><span class="sxs-lookup"><span data-stu-id="abea3-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="abea3-129">Invocar um método direto de um aplicativo back-end</span><span class="sxs-lookup"><span data-stu-id="abea3-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="abea3-130">Invocação de método</span><span class="sxs-lookup"><span data-stu-id="abea3-130">Method invocation</span></span>
<span data-ttu-id="abea3-131">Invocações de método direto em um dispositivo são chamadas HTTP, que compreendem:</span><span class="sxs-lookup"><span data-stu-id="abea3-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="abea3-132">Olá *URI* toohello específico de dispositivo (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="abea3-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="abea3-133">Olá POST *método*</span><span class="sxs-lookup"><span data-stu-id="abea3-133">hello POST *method*</span></span>
* <span data-ttu-id="abea3-134">*Cabeçalhos* que contêm autorização hello, ID, o tipo de conteúdo e a codificação do conteúdo de solicitação</span><span class="sxs-lookup"><span data-stu-id="abea3-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="abea3-135">JSON transparente *corpo* em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="abea3-135">A transparent JSON *body* in hello following format:</span></span>

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

<span data-ttu-id="abea3-136">Tempo limite em segundos.</span><span class="sxs-lookup"><span data-stu-id="abea3-136">Timeout is in seconds.</span></span> <span data-ttu-id="abea3-137">Se o tempo limite não for definida, o padrão é too30 segundos.</span><span class="sxs-lookup"><span data-stu-id="abea3-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="abea3-138">Resposta</span><span class="sxs-lookup"><span data-stu-id="abea3-138">Response</span></span>
<span data-ttu-id="abea3-139">aplicativo de back-end Olá recebe uma resposta que consiste em:</span><span class="sxs-lookup"><span data-stu-id="abea3-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="abea3-140">*Código de status HTTP*, que é usado para erros provenientes do hello IoT Hub, inclusive um erro 404 para dispositivos que não estão conectados</span><span class="sxs-lookup"><span data-stu-id="abea3-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="abea3-141">*Cabeçalhos* que contêm Olá ETag, ID, o tipo de conteúdo e a codificação do conteúdo de solicitação</span><span class="sxs-lookup"><span data-stu-id="abea3-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="abea3-142">JSON *corpo* em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="abea3-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="abea3-143">Ambos `status` e `body` são fornecidos pelo dispositivo hello e usado toorespond com código de status do dispositivo hello e/ou descrição.</span><span class="sxs-lookup"><span data-stu-id="abea3-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="abea3-144">Tratar um método direto em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="abea3-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="abea3-145">Invocação de método</span><span class="sxs-lookup"><span data-stu-id="abea3-145">Method invocation</span></span>
<span data-ttu-id="abea3-146">Dispositivos recebem solicitações de método direto no tópico MQTT hello:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="abea3-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="abea3-147">corpo da saudação qual dispositivo Olá recebe é em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="abea3-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="abea3-148">As solicitações de método são QoS 0.</span><span class="sxs-lookup"><span data-stu-id="abea3-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="abea3-149">Resposta</span><span class="sxs-lookup"><span data-stu-id="abea3-149">Response</span></span>
<span data-ttu-id="abea3-150">dispositivo Olá envia respostas muito`$iothub/methods/res/{status}/?$rid={request id}`, onde:</span><span class="sxs-lookup"><span data-stu-id="abea3-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="abea3-151">Olá `status` propriedade é status fornecido pelo dispositivo de saudação de execução do método.</span><span class="sxs-lookup"><span data-stu-id="abea3-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="abea3-152">Olá `$rid` propriedade é Olá solicitação ID de invocação de método hello recebida do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="abea3-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="abea3-153">corpo de saudação é definido pelo dispositivo hello e pode ser qualquer status.</span><span class="sxs-lookup"><span data-stu-id="abea3-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="abea3-154">Material de referência adicional</span><span class="sxs-lookup"><span data-stu-id="abea3-154">Additional reference material</span></span>
<span data-ttu-id="abea3-155">Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:</span><span class="sxs-lookup"><span data-stu-id="abea3-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="abea3-156">[Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="abea3-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="abea3-157">[Limitação e cotas] [ lnk-quotas] descreve cotas Olá que se aplicam a toohello serviço de IoT Hub e Olá limitação tooexpect de comportamento quando você usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="abea3-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="abea3-158">[SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub de vários idiomas.</span><span class="sxs-lookup"><span data-stu-id="abea3-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="abea3-159">[Linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens] [ lnk-query] descreve Olá linguagem de consulta de IoT Hub, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="abea3-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="abea3-160">[Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="abea3-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abea3-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abea3-161">Next steps</span></span>
<span data-ttu-id="abea3-162">Agora, você aprendeu como métodos de toouse direto, você pode estar interessado em Olá tópico de guia do desenvolvedor de IoT Hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="abea3-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="abea3-163">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="abea3-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="abea3-164">Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá seguindo o tutorial de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="abea3-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="abea3-165">[Usar métodos diretos][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="abea3-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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
