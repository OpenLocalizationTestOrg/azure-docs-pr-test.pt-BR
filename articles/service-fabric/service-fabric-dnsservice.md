---
title: "aaaAzure serviço DNS de malha do serviço | Microsoft Docs"
description: "Usar serviço de dns do Service Fabric para descobrir microservices de dentro do cluster de saudação."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="c2a6e-103">Serviço DNS no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2a6e-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="c2a6e-104">Olá serviço DNS é um serviço de sistema opcional que você pode habilitar no seu cluster toodiscover outros serviços usando o protocolo DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="c2a6e-105">Muitos serviços, especialmente em contêineres services, podem ter um nome de URL existente e ser capaz de tooresolve-los usar o protocolo de DNS padrão da saudação (em vez de protocolo de serviço de nomes de saudação) é desejável, particularmente em cenários de "comparar e deslocar".</span><span class="sxs-lookup"><span data-stu-id="c2a6e-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="c2a6e-106">Olá serviço DNS permite que você toomap DNS nomes tooa nome do serviço e, portanto, resolva endereços IP do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="c2a6e-107">Olá serviço DNS mapeia nomes tooservice nomes DNS, que por sua vez são resolvidos pelo ponto de extremidade do hello Naming Service tooreturn Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="c2a6e-108">nome DNS de saudação para serviço de saudação é fornecido no momento de saudação da criação.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![pontos de extremidade de serviço][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="c2a6e-110">Habilitar o serviço de DNS Olá</span><span class="sxs-lookup"><span data-stu-id="c2a6e-110">Enabling hello DNS service</span></span>
<span data-ttu-id="c2a6e-111">Primeiro você precisa de serviço DNS de Olá tooenable em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="c2a6e-112">Obter modelo Olá cluster Olá que você deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="c2a6e-113">Pode hello ou use [modelos de exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) ou criar um modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="c2a6e-114">Você pode habilitar o serviço DNS de saudação com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2a6e-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="c2a6e-115">Verifique que Olá `apiversion` está definido muito`2017-07-01-preview` para Olá `Microsoft.ServiceFabric/clusters` recursos e se não, atualizá-lo conforme Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2a6e-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="c2a6e-116">Agora ativar o serviço DNS de saudação adicionando Olá seguintes `addonFeatures` seção após Olá `fabricSettings` seção conforme Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2a6e-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="c2a6e-117">Depois de atualizar o modelo de cluster com hello anterior alterações, aplicá-los e permitem Olá atualização concluída.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="c2a6e-118">Uma vez concluído, Olá serviço de sistema DNS começa a ser executado no cluster que é chamado `fabric:/System/DnsService` na seção de serviço do sistema no Gerenciador do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="c2a6e-119">Como alternativa, você pode habilitar Olá serviço DNS por meio do portal Olá em tempo de saudação da criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="c2a6e-120">Olá serviço DNS pode ser habilitado, marcando a caixa de saudação `Include DNS service` em Olá `Cluster configuration` menu conforme Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2a6e-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![Habilitar o serviço do DNS por meio do portal Olá][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="c2a6e-122">Configurar nome DNS de saudação para seu serviço</span><span class="sxs-lookup"><span data-stu-id="c2a6e-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="c2a6e-123">Quando Olá serviço DNS estiver em execução no cluster, você pode definir um nome DNS para seus serviços declarativamente para serviços padrão em Olá `ApplicationManifest.xml` ou por meio de comandos do Powershell.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="c2a6e-124">Nome DNS de saudação para um serviço padrão da configuração na Olá ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="c2a6e-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="c2a6e-125">Abra seu projeto no Visual Studio ou seu editor favorito e Olá `ApplicationManifest.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="c2a6e-126">Vá toohello seção de serviços padrão e para cada saudação de adicionar serviço `ServiceDnsName` atributo.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="c2a6e-127">saudação de exemplo a seguir mostra como tooset Olá nome DNS do serviço de saudação muito`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="c2a6e-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="c2a6e-128">Depois que o aplicativo hello é implantado, instância de serviço de saudação no hello Service Fabric explorer mostra nome DNS de saudação nessa instância, conforme mostrado na figura a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="c2a6e-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![pontos de extremidade de serviço][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="c2a6e-130">Configurar nome DNS de saudação para um serviço usando o Powershell</span><span class="sxs-lookup"><span data-stu-id="c2a6e-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="c2a6e-131">Você pode definir o nome DNS de saudação para um serviço ao criá-la usando Olá `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="c2a6e-132">Olá exemplo a seguir cria um novo serviço sem monitoração de estado com o nome DNS Olá`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="c2a6e-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a><span data-ttu-id="c2a6e-133">Usando o DNS nos serviços</span><span class="sxs-lookup"><span data-stu-id="c2a6e-133">Using DNS in your services</span></span>
<span data-ttu-id="c2a6e-134">Se você implantar mais de um serviço, você pode encontrar pontos de extremidade de saudação do toocommunicate outros serviços com usando um nome DNS.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="c2a6e-135">Olá serviço DNS só é aplicável toostateless serviços, como Olá protocolo DNS não pode se comunicar com os serviços com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="c2a6e-136">Para serviços com monitoração de estado, você pode usar o proxy reverso internos de saudação para http chamadas toocall uma partição de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="c2a6e-137">Olá código a seguir mostra como toocall outro serviço, que é simplesmente um http regular chamar onde você pode fornecer a porta de saudação e qualquer caminho opcional como parte da URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2a6e-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c2a6e-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2a6e-138">Next steps</span></span>
<span data-ttu-id="c2a6e-139">Saiba mais sobre a comunicação de serviço em cluster Olá com [se conectar e se comunicar com serviços](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="c2a6e-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
