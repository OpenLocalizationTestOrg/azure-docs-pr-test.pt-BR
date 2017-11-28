---
title: "Diagnóstico de proxy reverso do Azure Service Fabric | Microsoft Docs"
description: "Saiba como monitorar e diagnosticar o processamento de solicitação no proxy reverso."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 3bc631606afbc93d5bca94f4955fd2ef816fa9fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-request-processing-at-the-reverse-proxy"></a><span data-ttu-id="b14e8-103">Monitorar e diagnosticar o processamento de solicitação no proxy reverso</span><span class="sxs-lookup"><span data-stu-id="b14e8-103">Monitor and diagnose request processing at the reverse proxy</span></span>

<span data-ttu-id="b14e8-104">A partir da versão 5.7 do Service Fabric, os eventos de métrica de carga e integridade estão disponíveis para coleta.</span><span class="sxs-lookup"><span data-stu-id="b14e8-104">Starting with the 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="b14e8-105">Os eventos estão disponíveis em dois canais, um somente com eventos de erro relacionados à falha no processamento da solicitação no proxy reverso e outro contendo eventos detalhados com entradas de solicitações bem-sucedidas e com falha.</span><span class="sxs-lookup"><span data-stu-id="b14e8-105">The events are available in two channels, one with only error events related to request processing failure at the reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="b14e8-106">Confira [Coletar eventos de proxy reverso](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) para habilitar a coleta de eventos desses canais nos clusters locais e do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b14e8-106">Refer to [Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) to enable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="b14e8-107">Solucionar problemas usando logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b14e8-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="b14e8-108">Aqui estão alguns exemplos de como interpretar os logs de falha comuns que podem ser encontrados:</span><span class="sxs-lookup"><span data-stu-id="b14e8-108">Here are some examples on how to interpret the common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="b14e8-109">Proxy reverso retorna código de status de resposta 504 (tempo limite).</span><span class="sxs-lookup"><span data-stu-id="b14e8-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="b14e8-110">Um motivo pode ser que o serviço não responde dentro do período de tempo limite da solicitação.</span><span class="sxs-lookup"><span data-stu-id="b14e8-110">One reason could be due to the service failing to reply within the request timeout period.</span></span>
<span data-ttu-id="b14e8-111">O primeiro evento abaixo registra os detalhes da solicitação recebida no proxy reverso.</span><span class="sxs-lookup"><span data-stu-id="b14e8-111">The first event below logs the details of the request received at the reverse proxy.</span></span> <span data-ttu-id="b14e8-112">O segundo evento indica que a solicitação falhou no encaminhamento para o serviço devido a "internal error = ERROR_WINHTTP_TIMEOUT"</span><span class="sxs-lookup"><span data-stu-id="b14e8-112">The second event indicates that the request failed while forwarding to service, due to "internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="b14e8-113">A carga inclui:</span><span class="sxs-lookup"><span data-stu-id="b14e8-113">The payload includes:</span></span>

    *  <span data-ttu-id="b14e8-114">**traceId**: esse GUID pode ser usado para correlacionar todos os eventos correspondentes a uma mesma solicitação.</span><span class="sxs-lookup"><span data-stu-id="b14e8-114">**traceId**: This GUID can be used to correlate all the events corresponding to a single request.</span></span> <span data-ttu-id="b14e8-115">Nos dois eventos abaixo, traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, indicando que pertencem à mesma solicitação.</span><span class="sxs-lookup"><span data-stu-id="b14e8-115">In the below two events, the traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong to the same request.</span></span>
    *  <span data-ttu-id="b14e8-116">**requestUrl**: a URL (URL de Proxy Reverso) à qual a solicitação foi enviada.</span><span class="sxs-lookup"><span data-stu-id="b14e8-116">**requestUrl**: The URL (Reverse proxy URL) to which the request was sent.</span></span>
    *  <span data-ttu-id="b14e8-117">**verb**: verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="b14e8-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="b14e8-118">**remoteAddress**: endereço do cliente que envia a solicitação.</span><span class="sxs-lookup"><span data-stu-id="b14e8-118">**remoteAddress**: Address of client sending the request.</span></span>
    *  <span data-ttu-id="b14e8-119">**resolvedServiceUrl**: URL de ponto de extremidade de serviço para a qual a solicitação de entrada foi resolvida.</span><span class="sxs-lookup"><span data-stu-id="b14e8-119">**resolvedServiceUrl**: Service endpoint URL to which the incoming request was resolved.</span></span> 
    *  <span data-ttu-id="b14e8-120">**errorDetails**: informações adicionais sobre a falha.</span><span class="sxs-lookup"><span data-stu-id="b14e8-120">**errorDetails**: Additional information about the failure.</span></span>

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request to service: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. <span data-ttu-id="b14e8-121">Proxy reverso retorna código de status de resposta 404 (não encontrado).</span><span class="sxs-lookup"><span data-stu-id="b14e8-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="b14e8-122">Eis um evento de exemplo em que o proxy reverso retorna 404, já que não conseguiu localizar o ponto de extremidade de serviço correspondente.</span><span class="sxs-lookup"><span data-stu-id="b14e8-122">Here is an example event where reverse proxy returns 404 since it failed to find the matching service endpoint.</span></span>
    <span data-ttu-id="b14e8-123">As entradas de carga de interesse aqui são:</span><span class="sxs-lookup"><span data-stu-id="b14e8-123">The payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="b14e8-124">**processRequestPhase**: indica a fase durante o processamento da solicitação em que a falha ocorreu, ***TryGetEndpoint***, ou seja,</span><span class="sxs-lookup"><span data-stu-id="b14e8-124">**processRequestPhase**: Indicates the phase during request processing when the failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="b14e8-125">durante a tentativa de buscar o ponto de extremidade de serviço para encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="b14e8-125">while trying to fetch the service endpoint to forward to.</span></span> 
    *  <span data-ttu-id="b14e8-126">**errorDetails**: lista os critérios de pesquisa de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="b14e8-126">**errorDetails**: Lists the endpoint search criteria.</span></span> <span data-ttu-id="b14e8-127">Aqui você pode ver que o listenerName especificado = **FrontEndListener**, enquanto a lista de ponto de extremidade de réplica contém somente um ouvinte com o nome **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="b14e8-127">Here you can see that the listenerName specified = **FrontEndListener** whereas the replica endpoint list only contains a listener with the name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward to service: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    <span data-ttu-id="b14e8-128">Outro exemplo em que o proxy reverso pode retornar 404 Não Encontrado é: parâmetro de configuração ApplicationGateway\Http **SecureOnlyMode** está definido como true, com um proxy inverso escutando **HTTPS**; no entanto, nenhum ponto de extremidade de réplica é seguro (escutando HTTP).</span><span class="sxs-lookup"><span data-stu-id="b14e8-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set to true with the reverse proxy listening on **HTTPS**, however all of the replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="b14e8-129">Proxy reverso retorna 404, já que não consegue localizar um ponto de extremidade de escuta HTTPS para encaminhar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="b14e8-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS to forward the request.</span></span> <span data-ttu-id="b14e8-130">A análise dos parâmetros na carga do evento ajuda a delimitar o problema:</span><span class="sxs-lookup"><span data-stu-id="b14e8-130">Analyzing the parameters in the event payload helps to narrow down the issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="b14e8-131">Falha na solicitação para o proxy reverso com erro de tempo limite.</span><span class="sxs-lookup"><span data-stu-id="b14e8-131">Request to the reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="b14e8-132">Os logs de evento contêm um evento com os detalhes da solicitação recebida (não mostrados aqui).</span><span class="sxs-lookup"><span data-stu-id="b14e8-132">The event logs contain an event with the received request details (not shown here).</span></span>
    <span data-ttu-id="b14e8-133">O próximo evento mostra que o serviço respondeu com um código de status 404 e o proxy reverso inicia uma ação de resolver novamente.</span><span class="sxs-lookup"><span data-stu-id="b14e8-133">The next event shows that the service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request to service returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    <span data-ttu-id="b14e8-134">Ao coletar todos os eventos, você verá uma cadeia de eventos mostrando cada resolução e a tentativa de encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="b14e8-134">When collecting all the events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="b14e8-135">O último evento na série mostra que o processamento de solicitação falhou alcançando o tempo limite, juntamente com o número de tentativas de resolução com êxito.</span><span class="sxs-lookup"><span data-stu-id="b14e8-135">The last event in the series shows the request processing has failed with a timeout, along with the number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b14e8-136">É recomendável manter a coleta de eventos do canal detalhado desabilitada por padrão e habilitá-la para a solução de problemas caso a caso.</span><span class="sxs-lookup"><span data-stu-id="b14e8-136">It is recommended to keep the  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    <span data-ttu-id="b14e8-137">Se a coleta está habilitada somente para eventos de erro/crítico, você verá um evento com detalhes sobre o tempo limite e o número de tentativas de resolução.</span><span class="sxs-lookup"><span data-stu-id="b14e8-137">If collection is enabled for critical/error events only, you see one event with details about the timeout and the number of resolve attempts.</span></span> 
    
    <span data-ttu-id="b14e8-138">Se o serviço pretende enviar um código de status 404 para o usuário, ele deve vir acompanhado de um cabeçalho "X-ServiceFabric".</span><span class="sxs-lookup"><span data-stu-id="b14e8-138">If the service intends to send a 404 status code back to the user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="b14e8-139">Depois de corrigir isso, você verá que o proxy reverso encaminha o código de status para o cliente.</span><span class="sxs-lookup"><span data-stu-id="b14e8-139">After fixing this, you will see that reverse proxy forwards the status code back to the client.</span></span>  

4. <span data-ttu-id="b14e8-140">Casos em que o cliente desconectou a solicitação.</span><span class="sxs-lookup"><span data-stu-id="b14e8-140">Cases when the client has disconnected the request.</span></span>

    <span data-ttu-id="b14e8-141">O evento abaixo é registrado quando o proxy reverso está encaminhando a resposta ao cliente, mas o cliente se desconecta:</span><span class="sxs-lookup"><span data-stu-id="b14e8-141">The below event is recorded when reverse proxy is forwarding the response to client but the client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable to send response to client: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> <span data-ttu-id="b14e8-142">Eventos relacionados ao processamento de solicitação de websocket não estão registrados em log no momento.</span><span class="sxs-lookup"><span data-stu-id="b14e8-142">Events related to websocket request processing are not currently logged.</span></span> <span data-ttu-id="b14e8-143">Isso será adicionado na próxima versão.</span><span class="sxs-lookup"><span data-stu-id="b14e8-143">This will be added in the next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b14e8-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b14e8-144">Next steps</span></span>
* <span data-ttu-id="b14e8-145">[Agregação e coleta de eventos usando o Diagnóstico do Microsoft Azure](service-fabric-diagnostics-event-aggregation-wad.md) para habilitar a coleta de logs em clusters do Azure.</span><span class="sxs-lookup"><span data-stu-id="b14e8-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="b14e8-146">Para exibir eventos do Service Fabric no Visual Studio, confira [Monitorar e diagnosticar localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="b14e8-146">To view Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="b14e8-147">Consulte [Configurar o proxy reverso para se conectar aos serviços seguros](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) para obter exemplos de modelo do Azure Resource Manager a fim de configurar o proxy reverso seguro com as diferentes opções de validação de certificado do serviço.</span><span class="sxs-lookup"><span data-stu-id="b14e8-147">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="b14e8-148">Leia [Proxy reverso do Service Fabric](service-fabric-reverseproxy.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="b14e8-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) to learn more.</span></span>
