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
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>Monitorar e diagnosticar o processamento de solicitação no proxy reverso Olá

Começando com a versão 5.7 de saudação do Service Fabric, eventos de proxy reverso estão disponíveis para a coleção. eventos de saudação estão disponíveis nos dois canais, uma com apenas os eventos de erro relacionadas toorequest falha de processamento no proxy reverso hello e segundo canal contendo eventos detalhados com entradas de solicitações bem-sucedidas e com falha.

Consulte também[coletar eventos de proxy reverso](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable coletando eventos desses canais no local e clusters de malha do serviço do Azure.

## <a name="troubleshoot-using-diagnostics-logs"></a>Solucionar problemas usando logs de diagnóstico
Aqui estão alguns exemplos sobre como logs de falha comuns toointerpret Olá um pode encontrar:

1. Proxy reverso retorna código de status de resposta 504 (tempo limite).

    Um motivo pode ser devido a falha do serviço toohello tooreply dentro do período de espera de solicitação de saudação.
Olá primeiro evento abaixo registra os detalhes de saudação do hello solicitação recebida no proxy reverso hello. Hello segundo evento indica que a solicitação Olá falhou ao tooservice de encaminhamento devido muito "Erro interno = ERROR_WINHTTP_TIMEOUT" 

    carga de saudação inclui:

    *  **traceId**: esse GUID pode ser usado toocorrelate todos os eventos de saudação correspondente tooa única solicitação. Em Olá abaixo dois eventos, Olá traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, indicando que eles pertencem toohello mesma solicitação.
    *  **requestUrl**: Olá URL (URL de proxy reverso) toowhich Olá solicitação foi enviada.
    *  **verb**: verbo HTTP.
    *  **remoteAddress**: endereço de envio de solicitação de saudação do cliente.
    *  **resolvedServiceUrl**: serviço ponto de extremidade URL toowhich Olá solicitação de entrada foi resolvida. 
    *  **errorDetails**: informações adicionais sobre a falha de saudação.

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

2. Proxy reverso retorna código de status de resposta 404 (não encontrado). 
    
    Aqui está um evento de exemplo em que o proxy inverso retorna 404 porque ele falhou Olá toofind correspondência de ponto de extremidade de serviço.
    Olá carga entradas de interesse aqui mencionados são:
    *  **processRequestPhase**: indica a fase Olá durante o processamento da solicitação quando ocorreu a falha de hello, ***TryGetEndpoint*** ou seja ao tentar toofetch Olá serviço ponto de extremidade tooforward para. 
    *  **errorDetails**: lista de critérios de pesquisa de ponto de extremidade de saudação. Aqui você pode ver que listenerName Olá especificado = **FrontEndListener** enquanto a lista de ponto de extremidade de réplica Olá contém apenas um ouvinte com o nome da saudação **OldListener**.
    
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
    Outro exemplo em que o proxy reverso pode retornar 404 não encontrados é: o parâmetro de configuração ApplicationGateway\Http **SecureOnlyMode** definida tootrue com escuta de proxy reverso do hello **HTTPS**, No entanto, todos os pontos de extremidade de réplica Olá são não seguros (escuta HTTP).
    Inverta retorna proxy 404 porque não é possível localizar um ponto de extremidade escutando em uma solicitação de saudação tooforward HTTPS. Analisar parâmetros Olá na carga do evento Olá ajuda toonarrow problema hello:
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. Proxy reverso de toohello de solicitação falha com um erro de tempo limite. 
    logs de eventos de saudação contêm um evento com detalhes de solicitação recebida de saudação (não mostrados aqui).
    próximo evento a saudação mostra que o serviço Olá respondeu com um código de 404 status e proxy reverso inicia um resolver novamente. 

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
    Ao coletar todos os eventos de hello, você verá um treinamento de mostrando cada resolução e a tentativa de encaminhamento de eventos.
    último evento Olá em série Olá mostra o processamento da solicitação Olá falhou com um tempo limite, juntamente com número de saudação de tentativas de resolver com êxito.
    
    > [!NOTE]
    > Ele é recomendado a coleta de eventos de canal detalhado Olá tookeep desabilitada por padrão e habilitá-la para solução de problemas em uma base de necessidade.

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
    
    Se a coleção está habilitada para eventos de erro/crítico apenas, você verá um evento com detalhes sobre o tempo limite de saudação e número de saudação de tentativas de resolver. 
    
    Se o serviço de saudação pretenda toosend um usuário de toohello voltar do código de 404 status, ele deve vir acompanhado de um cabeçalho "X-ServiceFabric". Depois de corrigir isso, você verá esse proxy reverso encaminhamentos Olá status código back toohello cliente.  

4. Casos quando Olá cliente se desconectou Olá solicitação.

    Olá abaixo o evento é registrado quando o proxy reverso está encaminhando Olá resposta tooclient mas Olá cliente se desconecta:

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
> Processamento de solicitação de toowebsocket relacionados de eventos não está conectado no momento. Isso será adicionado na próxima versão do hello.

## <a name="next-steps"></a>Próximas etapas
* [Agregação e coleta de eventos usando o Diagnóstico do Microsoft Azure](service-fabric-diagnostics-event-aggregation-wad.md) para habilitar a coleta de logs em clusters do Azure.
* eventos do Service Fabric tooview no Visual Studio, consulte [monitorar e diagnosticar localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
* Consulte também[configurar proxy reverso tooconnect toosecure serviços](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) para o Azure Resource Manager proxy reverso segura de tooconfigure com opções de validação de certificado de serviço diferentes Olá amostras de modelo.
* Leitura [proxy reverso do Service Fabric](service-fabric-reverseproxy.md) toolearn mais.
