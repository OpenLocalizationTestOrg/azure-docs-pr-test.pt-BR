---
title: "aaaAzure Service Fabric Inverter comunicação segura proxy | Microsoft Docs"
description: "Configure a comunicação de ponta a ponta proxy reverso tooenable segura."
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
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Conecte-se o serviço seguro tooa com proxy reverso Olá

Este artigo explica como tooestablish proteger a conexão entre o proxy reverso hello e serviços, permitindo que um canal seguro de tooend final.

Conectando a serviços toosecure é suportado apenas quando o proxy reverso é toolisten configurado em HTTPS. Restante do documento hello supõe que esse é o caso de saudação.
Consulte também[proxy no Azure Service Fabric reverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure proxy reverso do hello na malha do serviço.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Estabelecimento de conexão segura entre o proxy reverso hello e serviços 

### <a name="reverse-proxy-authenticating-tooservices"></a>Inverter tooservices de autenticação de proxy:
Olá proxy reverso se identifica tooservices usando seu certificado, especificado com ***reverseProxyCertificate*** propriedade Olá **Cluster** [seção de tipo de recurso](../azure-resource-manager/resource-group-authoring-templates.md). Serviços podem implementar o certificado de saudação do hello lógica tooverify apresentado pelo proxy reverso hello. Serviços de saudação podem especificar detalhes do certificado de cliente de saudação aceitada como definições de configuração no pacote de configuração de saudação. Isso pode ser lida em tempo de execução e usado toovalidate Olá certificado apresentado pelo proxy reverso hello. Consulte também[gerenciar parâmetros do aplicativo](service-fabric-manage-multiple-environment-app-configuration.md) tooadd definições de configuração de saudação. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>Reverte a verificar a identidade do serviço Olá via Olá certificado apresentado pelo serviço de saudação do proxy:
tooperform a validação de certificado do servidor de certificados Olá apresentado pelos serviços Olá, proxy reverso dá suporte a uma saudação as opções a seguir: None, ServiceCommonNameAndIssuer e ServiceCertificateThumbprints.
tooselect uma dessas três opções, especifique Olá **ApplicationCertificateValidationPolicy** na seção de parâmetros de saudação do elemento de ApplicationGateway/Http em [fabricSettings](service-fabric-cluster-fabric-settings.md).

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

Para obter detalhes sobre a configuração adicional para cada uma dessas opções, consulte toohello próxima seção.

### <a name="service-certificate-validation-options"></a>Opções de validação do certificado de serviço 

- **Nenhum**: proxy reverso ignora a verificação Olá delegadas do certificado de serviço e estabelece a conexão segura hello. Este é o comportamento padrão de saudação.
Especifique a saudação **ApplicationCertificateValidationPolicy** com valor **nenhum** na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.

- **ServiceCommonNameAndIssuer**: proxy reverso verifica o certificado Olá apresentado pelo serviço de saudação com base no nome comum do certificado e a impressão digital de imediato do emissor: especificar Olá **ApplicationCertificateValidationPolicy**  com valor **ServiceCommonNameAndIssuer** na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

lista de saudação toospecify de nome comum de serviço e as impressões digitais de emissor, adicione um **Http/ApplicationGateway/ServiceCommonNameAndIssuer** elemento sob fabricSettings, conforme mostrado abaixo. Vários nome comum do certificado e pares de impressão digital do emissor podem ser adicionados no elemento de matriz de parâmetros de saudação. 

Se proxy reverso do ponto de extremidade de saudação estiver se conectando a um certificado que é comum de toopresents nome e o emissor a impressão digital corresponde a qualquer um dos valores de saudação especificados aqui, canal SSL é estabelecido. Após os detalhes da falha toomatch Olá certificado, proxy reverso falha Olá solicitação de cliente com um código de status 502 (Gateway incorreto). saudação de linha de status HTTP também conterá frase hello "Certificado SSL inválido." 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- **ServiceCertificateThumbprints**: proxy reverso verificará se o certificado de serviço de proxy de saudação com base em sua impressão digital. Você pode escolher toogo essa rota ao Olá serviços estão configurados com certificados auto-assinados: especificar Olá **ApplicationCertificateValidationPolicy** com valor **ServiceCertificateThumbprints**na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

Também especificar impressões digitais de saudação com um **ServiceCertificateThumbprints** entrada na seção de parâmetros de elemento de ApplicationGateway/Http. Impressões digitais vários podem ser especificados como uma lista separada por vírgulas no campo de valor hello, conforme mostrado abaixo:

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

Se a impressão digital de Olá Olá do certificado do servidor está listado nesta entrada de configuração, o proxy reverso terá êxito conexão de SSL hello. Caso contrário, ele termina a conexão de saudação e falhar Olá solicitação do cliente com um 502 (Gateway incorreto). saudação de linha de status HTTP também conterá frase hello "Certificado SSL inválido."

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>Lógica de seleção do ponto de extremidade quando os serviços expõem pontos de extremidade seguros e inseguros
O Service Fabric oferece suporte à configuração de vários pontos de extremidade para um serviço. Confira [Especificar recursos em um manifesto do serviço](service-fabric-service-manifest-resources.md).

Proxy reverso seleciona uma saudação pontos de extremidade tooforward Olá solicitação com base em Olá **ListenerName** parâmetro de consulta. Se não for especificado, ele pode escolher qualquer ponto de extremidade da lista de pontos de extremidade de saudação. Pode ser um ponto de extremidade HTTP ou HTTPS. Pode haver requisitos/cenários em que você deseja toooperate de proxy reverso Olá no "modo de segurança somente", ou seja Você não quer Olá segura de proxy reverso tooforward solicitações toounsecured pontos de extremidade. Isso pode ser feito especificando Olá **SecureOnlyMode** entrada de configuração com o valor **true** na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> Ao operar em **SecureOnlyMode**, se o cliente tiver especificado um **ListenerName** correspondente tooan HTTP(unsecured) endpoint, falha de proxy reverso solicitação Olá com um código de status 404 (não encontrado) HTTP.

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>Configurando a autenticação de certificado de cliente por meio do proxy reverso Olá
Terminação SSL ocorre no proxy reverso hello e todos os dados do certificado de cliente hello serão perdidos. Olá serviços tooperform certificado para autenticação de cliente, definir Olá **ForwardClientCertificate** configuração na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.

1. Quando **ForwardClientCertificate** está definido muito**false**, inversa proxy não solicitará Olá certificado de cliente durante o handshake SSL com o cliente hello.
Este é o comportamento padrão de saudação.

2. Quando **ForwardClientCertificate** está definido muito**true**, reverter solicitações de proxy para o certificado do cliente Olá durante o handshake SSL com o cliente de saudação.
Em seguida, encaminhará cliente Olá dados do certificado em um cabeçalho HTTP personalizado chamado **certificado de cliente X**. valor do cabeçalho de saudação é cadeia de formato PEM Olá codificada em base64 do certificado saudação do cliente. serviço Olá pode ter êxito/falhar Olá solicite com código de status apropriado depois de inspecionar os dados do certificado hello.
Se o cliente Olá não apresentar um certificado, o proxy reverso encaminha um cabeçalho vazio e deixe caso de Olá Olá serviço identificador.

> Proxy reverso é um mero encaminhador. Ele não executará nenhuma validação de certificado saudação do cliente.


## <a name="next-steps"></a>Próximas etapas
* Consulte também[configurar proxy reverso tooconnect toosecure serviços](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) para o Azure Resource Manager proxy reverso segura de tooconfigure com opções de validação de certificado de serviço diferentes Olá amostras de modelo.
* Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Comunicação remota de serviço com os Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [API Web que usa o OWIN nos Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Gerenciar certificados de cluster](service-fabric-cluster-security-update-certs-azure.md)
