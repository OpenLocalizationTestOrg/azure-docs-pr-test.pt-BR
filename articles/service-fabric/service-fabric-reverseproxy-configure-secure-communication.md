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
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="5d025-103">Conecte-se o serviço seguro tooa com proxy reverso Olá</span><span class="sxs-lookup"><span data-stu-id="5d025-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="5d025-104">Este artigo explica como tooestablish proteger a conexão entre o proxy reverso hello e serviços, permitindo que um canal seguro de tooend final.</span><span class="sxs-lookup"><span data-stu-id="5d025-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="5d025-105">Conectando a serviços toosecure é suportado apenas quando o proxy reverso é toolisten configurado em HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5d025-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="5d025-106">Restante do documento hello supõe que esse é o caso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d025-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="5d025-107">Consulte também[proxy no Azure Service Fabric reverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure proxy reverso do hello na malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="5d025-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="5d025-108">Estabelecimento de conexão segura entre o proxy reverso hello e serviços</span><span class="sxs-lookup"><span data-stu-id="5d025-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="5d025-109">Inverter tooservices de autenticação de proxy:</span><span class="sxs-lookup"><span data-stu-id="5d025-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="5d025-110">Olá proxy reverso se identifica tooservices usando seu certificado, especificado com ***reverseProxyCertificate*** propriedade Olá **Cluster** [seção de tipo de recurso](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5d025-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="5d025-111">Serviços podem implementar o certificado de saudação do hello lógica tooverify apresentado pelo proxy reverso hello.</span><span class="sxs-lookup"><span data-stu-id="5d025-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="5d025-112">Serviços de saudação podem especificar detalhes do certificado de cliente de saudação aceitada como definições de configuração no pacote de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d025-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="5d025-113">Isso pode ser lida em tempo de execução e usado toovalidate Olá certificado apresentado pelo proxy reverso hello.</span><span class="sxs-lookup"><span data-stu-id="5d025-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="5d025-114">Consulte também[gerenciar parâmetros do aplicativo](service-fabric-manage-multiple-environment-app-configuration.md) tooadd definições de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d025-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="5d025-115">Reverte a verificar a identidade do serviço Olá via Olá certificado apresentado pelo serviço de saudação do proxy:</span><span class="sxs-lookup"><span data-stu-id="5d025-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="5d025-116">tooperform a validação de certificado do servidor de certificados Olá apresentado pelos serviços Olá, proxy reverso dá suporte a uma saudação as opções a seguir: None, ServiceCommonNameAndIssuer e ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="5d025-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="5d025-117">tooselect uma dessas três opções, especifique Olá **ApplicationCertificateValidationPolicy** na seção de parâmetros de saudação do elemento de ApplicationGateway/Http em [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="5d025-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="5d025-118">Para obter detalhes sobre a configuração adicional para cada uma dessas opções, consulte toohello próxima seção.</span><span class="sxs-lookup"><span data-stu-id="5d025-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="5d025-119">Opções de validação do certificado de serviço</span><span class="sxs-lookup"><span data-stu-id="5d025-119">Service certificate validation options</span></span> 

- <span data-ttu-id="5d025-120">**Nenhum**: proxy reverso ignora a verificação Olá delegadas do certificado de serviço e estabelece a conexão segura hello.</span><span class="sxs-lookup"><span data-stu-id="5d025-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="5d025-121">Este é o comportamento padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d025-121">This is hello default behavior.</span></span>
<span data-ttu-id="5d025-122">Especifique a saudação **ApplicationCertificateValidationPolicy** com valor **nenhum** na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="5d025-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="5d025-123">**ServiceCommonNameAndIssuer**: proxy reverso verifica o certificado Olá apresentado pelo serviço de saudação com base no nome comum do certificado e a impressão digital de imediato do emissor: especificar Olá **ApplicationCertificateValidationPolicy**  com valor **ServiceCommonNameAndIssuer** na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="5d025-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="5d025-124">lista de saudação toospecify de nome comum de serviço e as impressões digitais de emissor, adicione um **Http/ApplicationGateway/ServiceCommonNameAndIssuer** elemento sob fabricSettings, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5d025-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="5d025-125">Vários nome comum do certificado e pares de impressão digital do emissor podem ser adicionados no elemento de matriz de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d025-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="5d025-126">Se proxy reverso do ponto de extremidade de saudação estiver se conectando a um certificado que é comum de toopresents nome e o emissor a impressão digital corresponde a qualquer um dos valores de saudação especificados aqui, canal SSL é estabelecido.</span><span class="sxs-lookup"><span data-stu-id="5d025-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="5d025-127">Após os detalhes da falha toomatch Olá certificado, proxy reverso falha Olá solicitação de cliente com um código de status 502 (Gateway incorreto).</span><span class="sxs-lookup"><span data-stu-id="5d025-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="5d025-128">saudação de linha de status HTTP também conterá frase hello "Certificado SSL inválido."</span><span class="sxs-lookup"><span data-stu-id="5d025-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="5d025-129">**ServiceCertificateThumbprints**: proxy reverso verificará se o certificado de serviço de proxy de saudação com base em sua impressão digital.</span><span class="sxs-lookup"><span data-stu-id="5d025-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="5d025-130">Você pode escolher toogo essa rota ao Olá serviços estão configurados com certificados auto-assinados: especificar Olá **ApplicationCertificateValidationPolicy** com valor **ServiceCertificateThumbprints**na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="5d025-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="5d025-131">Também especificar impressões digitais de saudação com um **ServiceCertificateThumbprints** entrada na seção de parâmetros de elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="5d025-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="5d025-132">Impressões digitais vários podem ser especificados como uma lista separada por vírgulas no campo de valor hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="5d025-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

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

<span data-ttu-id="5d025-133">Se a impressão digital de Olá Olá do certificado do servidor está listado nesta entrada de configuração, o proxy reverso terá êxito conexão de SSL hello.</span><span class="sxs-lookup"><span data-stu-id="5d025-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="5d025-134">Caso contrário, ele termina a conexão de saudação e falhar Olá solicitação do cliente com um 502 (Gateway incorreto).</span><span class="sxs-lookup"><span data-stu-id="5d025-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="5d025-135">saudação de linha de status HTTP também conterá frase hello "Certificado SSL inválido."</span><span class="sxs-lookup"><span data-stu-id="5d025-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="5d025-136">Lógica de seleção do ponto de extremidade quando os serviços expõem pontos de extremidade seguros e inseguros</span><span class="sxs-lookup"><span data-stu-id="5d025-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="5d025-137">O Service Fabric oferece suporte à configuração de vários pontos de extremidade para um serviço.</span><span class="sxs-lookup"><span data-stu-id="5d025-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="5d025-138">Confira [Especificar recursos em um manifesto do serviço](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5d025-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="5d025-139">Proxy reverso seleciona uma saudação pontos de extremidade tooforward Olá solicitação com base em Olá **ListenerName** parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="5d025-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="5d025-140">Se não for especificado, ele pode escolher qualquer ponto de extremidade da lista de pontos de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d025-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="5d025-141">Pode ser um ponto de extremidade HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5d025-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="5d025-142">Pode haver requisitos/cenários em que você deseja toooperate de proxy reverso Olá no "modo de segurança somente", ou seja</span><span class="sxs-lookup"><span data-stu-id="5d025-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="5d025-143">Você não quer Olá segura de proxy reverso tooforward solicitações toounsecured pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="5d025-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="5d025-144">Isso pode ser feito especificando Olá **SecureOnlyMode** entrada de configuração com o valor **true** na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="5d025-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="5d025-145">Ao operar em **SecureOnlyMode**, se o cliente tiver especificado um **ListenerName** correspondente tooan HTTP(unsecured) endpoint, falha de proxy reverso solicitação Olá com um código de status 404 (não encontrado) HTTP.</span><span class="sxs-lookup"><span data-stu-id="5d025-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="5d025-146">Configurando a autenticação de certificado de cliente por meio do proxy reverso Olá</span><span class="sxs-lookup"><span data-stu-id="5d025-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="5d025-147">Terminação SSL ocorre no proxy reverso hello e todos os dados do certificado de cliente hello serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="5d025-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="5d025-148">Olá serviços tooperform certificado para autenticação de cliente, definir Olá **ForwardClientCertificate** configuração na seção de parâmetros de saudação do elemento de ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="5d025-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="5d025-149">Quando **ForwardClientCertificate** está definido muito**false**, inversa proxy não solicitará Olá certificado de cliente durante o handshake SSL com o cliente hello.</span><span class="sxs-lookup"><span data-stu-id="5d025-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="5d025-150">Este é o comportamento padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d025-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="5d025-151">Quando **ForwardClientCertificate** está definido muito**true**, reverter solicitações de proxy para o certificado do cliente Olá durante o handshake SSL com o cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d025-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="5d025-152">Em seguida, encaminhará cliente Olá dados do certificado em um cabeçalho HTTP personalizado chamado **certificado de cliente X**.</span><span class="sxs-lookup"><span data-stu-id="5d025-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="5d025-153">valor do cabeçalho de saudação é cadeia de formato PEM Olá codificada em base64 do certificado saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="5d025-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="5d025-154">serviço Olá pode ter êxito/falhar Olá solicite com código de status apropriado depois de inspecionar os dados do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="5d025-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="5d025-155">Se o cliente Olá não apresentar um certificado, o proxy reverso encaminha um cabeçalho vazio e deixe caso de Olá Olá serviço identificador.</span><span class="sxs-lookup"><span data-stu-id="5d025-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="5d025-156">Proxy reverso é um mero encaminhador.</span><span class="sxs-lookup"><span data-stu-id="5d025-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="5d025-157">Ele não executará nenhuma validação de certificado saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="5d025-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5d025-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d025-158">Next steps</span></span>
* <span data-ttu-id="5d025-159">Consulte também[configurar proxy reverso tooconnect toosecure serviços](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) para o Azure Resource Manager proxy reverso segura de tooconfigure com opções de validação de certificado de serviço diferentes Olá amostras de modelo.</span><span class="sxs-lookup"><span data-stu-id="5d025-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="5d025-160">Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="5d025-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="5d025-161">Comunicação remota de serviço com os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="5d025-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="5d025-162">API Web que usa o OWIN nos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="5d025-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="5d025-163">Gerenciar certificados de cluster</span><span class="sxs-lookup"><span data-stu-id="5d025-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
