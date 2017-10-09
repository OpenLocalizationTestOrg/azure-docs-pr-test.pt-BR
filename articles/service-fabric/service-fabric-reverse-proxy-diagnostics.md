---
title: "aaaAzure Service Fabric Inverter diagnóstico proxy | Microsoft Docs"
description: "Saiba como toomonitor e diagnosticar o processamento de solicitação no proxy reverso hello."
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
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a><span data-ttu-id="5e3cb-103">Monitorar e diagnosticar o processamento de solicitação no proxy reverso Olá</span><span class="sxs-lookup"><span data-stu-id="5e3cb-103">Monitor and diagnose request processing at hello reverse proxy</span></span>

<span data-ttu-id="5e3cb-104">Começando com a versão 5.7 de saudação do Service Fabric, eventos de proxy reverso estão disponíveis para a coleção.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-104">Starting with hello 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="5e3cb-105">eventos de saudação estão disponíveis nos dois canais, uma com apenas os eventos de erro relacionadas toorequest falha de processamento no proxy reverso hello e segundo canal contendo eventos detalhados com entradas de solicitações bem-sucedidas e com falha.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-105">hello events are available in two channels, one with only error events related toorequest processing failure at hello reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="5e3cb-106">Consulte também[coletar eventos de proxy reverso](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable coletando eventos desses canais no local e clusters de malha do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-106">Refer too[Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="5e3cb-107">Solucionar problemas usando logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="5e3cb-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="5e3cb-108">Aqui estão alguns exemplos sobre como logs de falha comuns toointerpret Olá um pode encontrar:</span><span class="sxs-lookup"><span data-stu-id="5e3cb-108">Here are some examples on how toointerpret hello common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="5e3cb-109">Proxy reverso retorna código de status de resposta 504 (tempo limite).</span><span class="sxs-lookup"><span data-stu-id="5e3cb-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="5e3cb-110">Um motivo pode ser devido a falha do serviço toohello tooreply dentro do período de espera de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-110">One reason could be due toohello service failing tooreply within hello request timeout period.</span></span>
<span data-ttu-id="5e3cb-111">Olá primeiro evento abaixo registra os detalhes de saudação do hello solicitação recebida no proxy reverso hello.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-111">hello first event below logs hello details of hello request received at hello reverse proxy.</span></span> <span data-ttu-id="5e3cb-112">Hello segundo evento indica que a solicitação Olá falhou ao tooservice de encaminhamento devido muito "Erro interno = ERROR_WINHTTP_TIMEOUT"</span><span class="sxs-lookup"><span data-stu-id="5e3cb-112">hello second event indicates that hello request failed while forwarding tooservice, due too"internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="5e3cb-113">carga de saudação inclui:</span><span class="sxs-lookup"><span data-stu-id="5e3cb-113">hello payload includes:</span></span>

    *  <span data-ttu-id="5e3cb-114">**traceId**: esse GUID pode ser usado toocorrelate todos os eventos de saudação correspondente tooa única solicitação.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-114">**traceId**: This GUID can be used toocorrelate all hello events corresponding tooa single request.</span></span> <span data-ttu-id="5e3cb-115">Em Olá abaixo dois eventos, Olá traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, indicando que eles pertencem toohello mesma solicitação.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-115">In hello below two events, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong toohello same request.</span></span>
    *  <span data-ttu-id="5e3cb-116">**requestUrl**: Olá URL (URL de proxy reverso) toowhich Olá solicitação foi enviada.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-116">**requestUrl**: hello URL (Reverse proxy URL) toowhich hello request was sent.</span></span>
    *  <span data-ttu-id="5e3cb-117">**verb**: verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="5e3cb-118">**remoteAddress**: endereço de envio de solicitação de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-118">**remoteAddress**: Address of client sending hello request.</span></span>
    *  <span data-ttu-id="5e3cb-119">**resolvedServiceUrl**: serviço ponto de extremidade URL toowhich Olá solicitação de entrada foi resolvida.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-119">**resolvedServiceUrl**: Service endpoint URL toowhich hello incoming request was resolved.</span></span> 
    *  <span data-ttu-id="5e3cb-120">**errorDetails**: informações adicionais sobre a falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-120">**errorDetails**: Additional information about hello failure.</span></span>

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
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
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

2. <span data-ttu-id="5e3cb-121">Proxy reverso retorna código de status de resposta 404 (não encontrado).</span><span class="sxs-lookup"><span data-stu-id="5e3cb-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="5e3cb-122">Aqui está um evento de exemplo em que o proxy inverso retorna 404 porque ele falhou Olá toofind correspondência de ponto de extremidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-122">Here is an example event where reverse proxy returns 404 since it failed toofind hello matching service endpoint.</span></span>
    <span data-ttu-id="5e3cb-123">Olá carga entradas de interesse aqui mencionados são:</span><span class="sxs-lookup"><span data-stu-id="5e3cb-123">hello payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="5e3cb-124">**processRequestPhase**: indica a fase Olá durante o processamento da solicitação quando ocorreu a falha de hello, ***TryGetEndpoint*** ou seja</span><span class="sxs-lookup"><span data-stu-id="5e3cb-124">**processRequestPhase**: Indicates hello phase during request processing when hello failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="5e3cb-125">ao tentar toofetch Olá serviço ponto de extremidade tooforward para.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-125">while trying toofetch hello service endpoint tooforward to.</span></span> 
    *  <span data-ttu-id="5e3cb-126">**errorDetails**: lista de critérios de pesquisa de ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-126">**errorDetails**: Lists hello endpoint search criteria.</span></span> <span data-ttu-id="5e3cb-127">Aqui você pode ver que listenerName Olá especificado = **FrontEndListener** enquanto a lista de ponto de extremidade de réplica Olá contém apenas um ouvinte com o nome da saudação **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-127">Here you can see that hello listenerName specified = **FrontEndListener** whereas hello replica endpoint list only contains a listener with hello name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
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
    <span data-ttu-id="5e3cb-128">Outro exemplo em que o proxy reverso pode retornar 404 não encontrados é: o parâmetro de configuração ApplicationGateway\Http **SecureOnlyMode** definida tootrue com escuta de proxy reverso do hello **HTTPS**, No entanto, todos os pontos de extremidade de réplica Olá são não seguros (escuta HTTP).</span><span class="sxs-lookup"><span data-stu-id="5e3cb-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set tootrue with hello reverse proxy listening on **HTTPS**, however all of hello replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="5e3cb-129">Inverta retorna proxy 404 porque não é possível localizar um ponto de extremidade escutando em uma solicitação de saudação tooforward HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS tooforward hello request.</span></span> <span data-ttu-id="5e3cb-130">Analisar parâmetros Olá na carga do evento Olá ajuda toonarrow problema hello:</span><span class="sxs-lookup"><span data-stu-id="5e3cb-130">Analyzing hello parameters in hello event payload helps toonarrow down hello issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="5e3cb-131">Proxy reverso de toohello de solicitação falha com um erro de tempo limite.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-131">Request toohello reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="5e3cb-132">logs de eventos de saudação contêm um evento com detalhes de solicitação recebida de saudação (não mostrados aqui).</span><span class="sxs-lookup"><span data-stu-id="5e3cb-132">hello event logs contain an event with hello received request details (not shown here).</span></span>
    <span data-ttu-id="5e3cb-133">próximo evento a saudação mostra que o serviço Olá respondeu com um código de 404 status e proxy reverso inicia um resolver novamente.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-133">hello next event shows that hello service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
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
    <span data-ttu-id="5e3cb-134">Ao coletar todos os eventos de hello, você verá um treinamento de mostrando cada resolução e a tentativa de encaminhamento de eventos.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-134">When collecting all hello events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="5e3cb-135">último evento Olá em série Olá mostra o processamento da solicitação Olá falhou com um tempo limite, juntamente com número de saudação de tentativas de resolver com êxito.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-135">hello last event in hello series shows hello request processing has failed with a timeout, along with hello number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5e3cb-136">Ele é recomendado a coleta de eventos de canal detalhado Olá tookeep desabilitada por padrão e habilitá-la para solução de problemas em uma base de necessidade.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-136">It is recommended tookeep hello  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

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
    
    <span data-ttu-id="5e3cb-137">Se a coleção está habilitada para eventos de erro/crítico apenas, você verá um evento com detalhes sobre o tempo limite de saudação e número de saudação de tentativas de resolver.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-137">If collection is enabled for critical/error events only, you see one event with details about hello timeout and hello number of resolve attempts.</span></span> 
    
    <span data-ttu-id="5e3cb-138">Se o serviço de saudação pretenda toosend um usuário de toohello voltar do código de 404 status, ele deve vir acompanhado de um cabeçalho "X-ServiceFabric".</span><span class="sxs-lookup"><span data-stu-id="5e3cb-138">If hello service intends toosend a 404 status code back toohello user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="5e3cb-139">Depois de corrigir isso, você verá esse proxy reverso encaminhamentos Olá status código back toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-139">After fixing this, you will see that reverse proxy forwards hello status code back toohello client.</span></span>  

4. <span data-ttu-id="5e3cb-140">Casos quando Olá cliente se desconectou Olá solicitação.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-140">Cases when hello client has disconnected hello request.</span></span>

    <span data-ttu-id="5e3cb-141">Olá abaixo o evento é registrado quando o proxy reverso está encaminhando Olá resposta tooclient mas Olá cliente se desconecta:</span><span class="sxs-lookup"><span data-stu-id="5e3cb-141">hello below event is recorded when reverse proxy is forwarding hello response tooclient but hello client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
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
> <span data-ttu-id="5e3cb-142">Processamento de solicitação de toowebsocket relacionados de eventos não está conectado no momento.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-142">Events related toowebsocket request processing are not currently logged.</span></span> <span data-ttu-id="5e3cb-143">Isso será adicionado na próxima versão do hello.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-143">This will be added in hello next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e3cb-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e3cb-144">Next steps</span></span>
* <span data-ttu-id="5e3cb-145">[Agregação e coleta de eventos usando o Diagnóstico do Microsoft Azure](service-fabric-diagnostics-event-aggregation-wad.md) para habilitar a coleta de logs em clusters do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="5e3cb-146">eventos do Service Fabric tooview no Visual Studio, consulte [monitorar e diagnosticar localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="5e3cb-146">tooview Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="5e3cb-147">Consulte também[configurar proxy reverso tooconnect toosecure serviços](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) para o Azure Resource Manager proxy reverso segura de tooconfigure com opções de validação de certificado de serviço diferentes Olá amostras de modelo.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-147">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="5e3cb-148">Leitura [proxy reverso do Service Fabric](service-fabric-reverseproxy.md) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="5e3cb-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) toolearn more.</span></span>
