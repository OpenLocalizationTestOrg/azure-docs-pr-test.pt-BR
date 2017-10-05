---
title: "Comunicação segura por proxy reverso do Azure Service Fabric | Microsoft Docs"
description: "Configure o proxy reverso para permitir a comunicação segura de ponta a ponta."
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
ms.openlocfilehash: 568f9638c59282bcd7d3fae058a1588a889c22dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a><span data-ttu-id="4a5af-103">Conectar-se a um serviço seguro com o proxy inverso</span><span class="sxs-lookup"><span data-stu-id="4a5af-103">Connect to a secure service with the reverse proxy</span></span>

<span data-ttu-id="4a5af-104">Este artigo explica como estabelecer uma conexão segura entre o proxy reverso e serviços, permitindo um canal seguro de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="4a5af-104">This article explains how to establish secure connection between the reverse proxy and services, thus enabling an end to end secure channel.</span></span>

<span data-ttu-id="4a5af-105">A conexão aos serviços seguros tem suporte apenas quando o proxy reverso é configurado para escutar em HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4a5af-105">Connecting to secure services is supported only when reverse proxy is configured to listen on HTTPS.</span></span> <span data-ttu-id="4a5af-106">O restante do documento supõe que esse é o caso.</span><span class="sxs-lookup"><span data-stu-id="4a5af-106">Rest of the document assumes this is the case.</span></span>
<span data-ttu-id="4a5af-107">Consulte [Proxy reverso no Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) para configurar o proxy reverso no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4a5af-107">Refer to [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) to configure the reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a><span data-ttu-id="4a5af-108">Estabelecimento de conexão segura entre o proxy reverso e os serviços</span><span class="sxs-lookup"><span data-stu-id="4a5af-108">Secure connection establishment between the reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-to-services"></a><span data-ttu-id="4a5af-109">Autenticação do proxy reverso nos serviços:</span><span class="sxs-lookup"><span data-stu-id="4a5af-109">Reverse proxy authenticating to services:</span></span>
<span data-ttu-id="4a5af-110">O proxy reverso identifica-se para os serviços usando seu certificado, que é especificado com a propriedade ***reverseProxyCertificate*** na seção **Cluster** [Tipo de recurso](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4a5af-110">The reverse proxy identifies itself to services using its certificate, specified with ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="4a5af-111">Os serviços podem implementar a lógica para verificar o certificado apresentado pelo proxy reverso.</span><span class="sxs-lookup"><span data-stu-id="4a5af-111">Services can implement the logic to verify the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="4a5af-112">Os serviços podem especificar os detalhes do certificado de cliente aceito como definições de configuração no pacote de configuração.</span><span class="sxs-lookup"><span data-stu-id="4a5af-112">The services can specify the accepted client certificate details as configuration settings in the configuration package.</span></span> <span data-ttu-id="4a5af-113">Isso pode ser lido em tempo de execução e usado para validar o certificado apresentado pelo proxy reverso.</span><span class="sxs-lookup"><span data-stu-id="4a5af-113">This can be read at runtime and used to validate the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="4a5af-114">Consulte [Gerenciar parâmetros do aplicativo](service-fabric-manage-multiple-environment-app-configuration.md) para adicionar as definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="4a5af-114">Refer to [Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) to add the configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a><span data-ttu-id="4a5af-115">Proxy reverso verificando a identidade do serviço por meio do certificado apresentado pelo serviço:</span><span class="sxs-lookup"><span data-stu-id="4a5af-115">Reverse proxy verifying the service's identity via the certificate presented by the service:</span></span>
<span data-ttu-id="4a5af-116">Para executar a validação de certificado do servidor dos certificados apresentados pelos serviços, o proxy reverso dá suporte a uma das seguintes opções: Nenhum, ServiceCommonNameAndIssuer e ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="4a5af-116">To perform server certificate validation of the certificates presented by the services, reverse proxy supports one of the following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="4a5af-117">Para selecionar uma dessas três opções, especifique o **ApplicationCertificateValidationPolicy** na seção de parâmetros do elemento ApplicationGateway/Http em [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="4a5af-117">To select one of these three options, specify the **ApplicationCertificateValidationPolicy** in the parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="4a5af-118">Consulte a próxima seção para obter detalhes sobre a configuração adicional para cada uma dessas opções.</span><span class="sxs-lookup"><span data-stu-id="4a5af-118">Refer to the next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="4a5af-119">Opções de validação do certificado de serviço</span><span class="sxs-lookup"><span data-stu-id="4a5af-119">Service certificate validation options</span></span> 

- <span data-ttu-id="4a5af-120">**Nenhum**: o proxy reverso ignora a verificação do certificado de serviço com proxy e estabelece a conexão segura.</span><span class="sxs-lookup"><span data-stu-id="4a5af-120">**None**: Reverse proxy skips verification of the proxied service certificate and establishes the secure connection.</span></span> <span data-ttu-id="4a5af-121">Esse é o comportamento padrão.</span><span class="sxs-lookup"><span data-stu-id="4a5af-121">This is the default behavior.</span></span>
<span data-ttu-id="4a5af-122">Especifique o **ApplicationCertificateValidationPolicy** com o valor **Nenhum** na seção de parâmetros do elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="4a5af-122">Specify the **ApplicationCertificateValidationPolicy** with value **None** in the parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="4a5af-123">**ServiceCommonNameAndIssuer**: o proxy reverso verifica o certificado apresentado pelo serviço com base no nome comum do certificado e a impressão digital do emissor imediato: especifique **ApplicationCertificateValidationPolicy** com o valor **ServiceCommonNameAndIssuer** na seção de parâmetros do elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="4a5af-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies the certificate presented by the service based on certificate's common name and immediate issuer's thumbprint: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="4a5af-124">Para especificar a lista de nomes de serviço comuns e as impressões digitais do emissor, adicione um elemento **Http/ApplicationGateway/ServiceCommonNameAndIssuer** em fabricSettings, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4a5af-124">To specify the list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="4a5af-125">É possível adicionar vários pares de nome de certificado comum e impressão digital do emissor no elemento da matriz dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4a5af-125">Multiple certificate common name and issuer thumbprint pairs can be added in the parameters array element.</span></span> 

<span data-ttu-id="4a5af-126">Se o proxy reverso do ponto de extremidade estiver se conectando para apresentar um certificado cujo nome comum e impressão digital do emissor correspondam a qualquer um dos valores especificados aqui, o canal SSL será estabelecido.</span><span class="sxs-lookup"><span data-stu-id="4a5af-126">If the endpoint reverse proxy is connecting to presents a certificate who's common name and  issuer thumbprint matches any of the values specified here, SSL channel is established.</span></span> <span data-ttu-id="4a5af-127">Em caso de falha de correspondência dos detalhes do certificado, a solicitação do cliente não será realizada pelo proxy reverso com um código de status 502 (Gateway incorreto).</span><span class="sxs-lookup"><span data-stu-id="4a5af-127">Upon failure to match the certificate details, reverse proxy fails the client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="4a5af-128">A linha de status HTTP também conterá a frase "Certificado SSL Inválido."</span><span class="sxs-lookup"><span data-stu-id="4a5af-128">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="4a5af-129">**ServiceCertificateThumbprints**: o proxy reverso verificará se o certificado de serviço com proxy tem base em sua impressão digital.</span><span class="sxs-lookup"><span data-stu-id="4a5af-129">**ServiceCertificateThumbprints**: Reverse proxy will verify the proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="4a5af-130">Você pode optar por acessar essa rota quando os serviços estiverem configurados com certificados autoassinados: especifique o **ApplicationCertificateValidationPolicy** com o valor **ServiceCertificateThumbprints** na seção de parâmetros do elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="4a5af-130">You can choose to go this route when the services are configured with self signed certificates: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="4a5af-131">Especifique também as impressões digitais com uma entrada **ServiceCertificateThumbprints** na seção de parâmetros do elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="4a5af-131">Also specify the thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="4a5af-132">É possível especificar várias impressões digitais como uma lista separada por vírgulas no campo de valor, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="4a5af-132">Multiple thumbprints can be specified as a comma-separated list in the value field, as shown below:</span></span>

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

<span data-ttu-id="4a5af-133">Se a impressão digital do certificado do servidor estiver listada nesta entrada de configuração, o proxy reverso terá êxito na conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="4a5af-133">If the thumbprint of the server certificate is listed in this config entry, reverse proxy succeeds the SSL connection.</span></span> <span data-ttu-id="4a5af-134">Caso contrário, ele encerrará a conexão e a solicitação do cliente falhará com um erro 502 (Gateway incorreto).</span><span class="sxs-lookup"><span data-stu-id="4a5af-134">Otherwise, it terminates the connection and fails the client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="4a5af-135">A linha de status HTTP também conterá a frase "Certificado SSL Inválido."</span><span class="sxs-lookup"><span data-stu-id="4a5af-135">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="4a5af-136">Lógica de seleção do ponto de extremidade quando os serviços expõem pontos de extremidade seguros e inseguros</span><span class="sxs-lookup"><span data-stu-id="4a5af-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="4a5af-137">O Service Fabric oferece suporte à configuração de vários pontos de extremidade para um serviço.</span><span class="sxs-lookup"><span data-stu-id="4a5af-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="4a5af-138">Confira [Especificar recursos em um manifesto do serviço](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4a5af-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="4a5af-139">O proxy reverso seleciona um dos pontos de extremidade para encaminhar a solicitação com base no parâmetro de consulta **ListenerName**.</span><span class="sxs-lookup"><span data-stu-id="4a5af-139">Reverse proxy selects one of the endpoints to forward the request based on the  **ListenerName** query parameter.</span></span> <span data-ttu-id="4a5af-140">Se isso não for especificado, ele poderá escolher qualquer ponto de extremidade da lista de pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="4a5af-140">If this is not specified, it can pick any endpoint from the endpoints list.</span></span> <span data-ttu-id="4a5af-141">Pode ser um ponto de extremidade HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4a5af-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="4a5af-142">Pode haver requisitos ou situações nas quais você deseja que o proxy reverso opere em um "modo somente de segurança", ou seja</span><span class="sxs-lookup"><span data-stu-id="4a5af-142">There might be scenarios/requirements where you want the reverse proxy to operate in a "secure only mode", i.e</span></span> <span data-ttu-id="4a5af-143">você não quer que o proxy reverso seguro encaminhe solicitações para pontos de extremidade não seguros.</span><span class="sxs-lookup"><span data-stu-id="4a5af-143">you don't want the secure reverse proxy to forward requests to unsecured endpoints.</span></span> <span data-ttu-id="4a5af-144">Isso pode ser feito especificando a entrada de configuração **SecureOnlyMode** com o valor **true** na seção de parâmetros do elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="4a5af-144">This can be achieved by specifying the **SecureOnlyMode** configuration entry with value **true** in the parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="4a5af-145">Ao operar em **SecureOnlyMode**, se o cliente tiver especificado um **ListenerName** correspondente a um ponto de extremidade HTTP(não seguro), a solicitação não será realizada pelo proxy reverso com um código de status HTTP 404 (Não Encontrado).</span><span class="sxs-lookup"><span data-stu-id="4a5af-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding to an HTTP(unsecured) endpoint, reverse proxy fails the request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a><span data-ttu-id="4a5af-146">Configurar a autenticação de certificado do cliente através do proxy reverso</span><span class="sxs-lookup"><span data-stu-id="4a5af-146">Setting up client certificate authentication through the reverse proxy</span></span>
<span data-ttu-id="4a5af-147">A terminação SSL ocorre no proxy reverso e todos os dados de certificado do cliente são perdidos.</span><span class="sxs-lookup"><span data-stu-id="4a5af-147">SSL termination happens at the reverse proxy and all the client certificate data is lost.</span></span> <span data-ttu-id="4a5af-148">Para que os serviços realizem a autenticação de certificado do cliente, defina a configuração **ForwardClientCertificate** na seção de parâmetros do elemento ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="4a5af-148">For the services to perform client certificate authentication, set the **ForwardClientCertificate** setting in the parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="4a5af-149">Quando **ForwardClientCertificate** for definido como **false**, o proxy reverso não solicitará o certificado de cliente durante o handshake de SSL com o cliente.</span><span class="sxs-lookup"><span data-stu-id="4a5af-149">When **ForwardClientCertificate** is set to **false**, reverse proxy will not request for the client certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="4a5af-150">Esse é o comportamento padrão.</span><span class="sxs-lookup"><span data-stu-id="4a5af-150">This is the default behavior.</span></span>

2. <span data-ttu-id="4a5af-151">Quando **ForwardClientCertificate** for definido como **true**, o proxy reverso solicitará o certificado de cliente durante o handshake de SSL com o cliente.</span><span class="sxs-lookup"><span data-stu-id="4a5af-151">When **ForwardClientCertificate** is set to **true**, reverse proxy requests for the client's certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="4a5af-152">Em seguida, ele encaminhará os dados do certificado do cliente em um cabeçalho HTTP personalizado chamado **X-Client-Certificate**.</span><span class="sxs-lookup"><span data-stu-id="4a5af-152">It will then forward the client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="4a5af-153">O valor do cabeçalho é a cadeia de formato PEM codificado em base64 do certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="4a5af-153">The header value is the base64 encoded PEM format string of the client's certificate.</span></span> <span data-ttu-id="4a5af-154">O serviço pode conseguir ou não atender à solicitação com o código de status apropriado depois de inspecionar os dados do certificado.</span><span class="sxs-lookup"><span data-stu-id="4a5af-154">The service can succeed/fail the request with appropriate status code after inspecting the certificate data.</span></span>
<span data-ttu-id="4a5af-155">Se o cliente não apresentar um certificado, o proxy reverso encaminhará um cabeçalho vazio e permitirá ao serviço lidar com o caso.</span><span class="sxs-lookup"><span data-stu-id="4a5af-155">If the client does not present a certificate, reverse proxy forwards an empty header and let the service handle the case.</span></span>

> <span data-ttu-id="4a5af-156">Proxy reverso é um mero encaminhador.</span><span class="sxs-lookup"><span data-stu-id="4a5af-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="4a5af-157">Ele não executará nenhuma validação de certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="4a5af-157">It will not perform any validation of the client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4a5af-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a5af-158">Next steps</span></span>
* <span data-ttu-id="4a5af-159">Consulte [Configurar o proxy reverso para se conectar aos serviços seguros](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) para obter exemplos de modelo do Azure Resource Manager a fim de configurar o proxy reverso seguro com as diferentes opções de validação de certificado do serviço.</span><span class="sxs-lookup"><span data-stu-id="4a5af-159">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="4a5af-160">Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4a5af-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="4a5af-161">Comunicação remota de serviço com os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="4a5af-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="4a5af-162">API Web que usa o OWIN nos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="4a5af-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="4a5af-163">Gerenciar certificados de cluster</span><span class="sxs-lookup"><span data-stu-id="4a5af-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
