---
title: "Serviço DNS do Azure Service Fabric | Microsoft Docs"
description: "Use o serviço DNS do Service Fabric para descobrir microsserviços no cluster."
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
ms.openlocfilehash: 9871bc5aa4e74ab0faef401d67c4e9558eb5e14b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="691cc-103">Serviço DNS no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="691cc-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="691cc-104">O Serviço DNS é um serviço do sistema opcional que pode ser habilitado no cluster para descobrir outros serviços usando o protocolo DNS.</span><span class="sxs-lookup"><span data-stu-id="691cc-104">The DNS Service is an optional system service that you can enable in your cluster to discover other services using the DNS protocol.</span></span>

<span data-ttu-id="691cc-105">Muitos serviços, especialmente serviços em contêineres, podem ter um nome de URL existente e ter a capacidade de resolvê-los usando o protocolo DNS padrão (em vez do protocolo do Serviço de Nomeação) é desejável, especialmente em cenários “lift-and-shift”.</span><span class="sxs-lookup"><span data-stu-id="691cc-105">Many services, especially containerized services, can have an existing URL name, and being able to resolve them using the standard DNS protocol (rather than the Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="691cc-106">O serviço DNS permite mapear nomes DNS para um nome de serviço e, portanto, resolver endereços IP do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="691cc-106">The DNS service enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="691cc-107">O serviço DNS mapeia nomes DNS para nomes de serviço, que por sua vez, são resolvidos pelo serviço de nomenclatura para retornar o ponto de extremidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="691cc-107">The DNS service maps DNS names to service names, which in turn are resolved by the Naming Service to return the service endpoint.</span></span> <span data-ttu-id="691cc-108">O nome DNS do serviço é fornecido no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="691cc-108">The DNS name for the service is provided at the time of creation.</span></span> 

![pontos de extremidade de serviço][0]

## <a name="enabling-the-dns-service"></a><span data-ttu-id="691cc-110">Habilitando o serviço DNS</span><span class="sxs-lookup"><span data-stu-id="691cc-110">Enabling the DNS service</span></span>
<span data-ttu-id="691cc-111">Primeiro, você precisa habilitar o serviço DNS no cluster.</span><span class="sxs-lookup"><span data-stu-id="691cc-111">First you need to enable the DNS service in your cluster.</span></span> <span data-ttu-id="691cc-112">Obtenha o modelo para o cluster que você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="691cc-112">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="691cc-113">Use os [modelos de exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) ou crie um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="691cc-113">You can either use the [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="691cc-114">Habilite o serviço DNS com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="691cc-114">You can enable the DNS service with the following steps:</span></span>

1. <span data-ttu-id="691cc-115">Verifique se a `apiversion` está definida como `2017-07-01-preview` para o recurso `Microsoft.ServiceFabric/clusters`, conforme mostrado neste trecho:</span><span class="sxs-lookup"><span data-stu-id="691cc-115">Check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in the following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="691cc-116">Agora, habilite o serviço DNS adicionando a seção `addonFeatures` a seguir após a seção `fabricSettings`, conforme mostrado neste trecho:</span><span class="sxs-lookup"><span data-stu-id="691cc-116">Now enable the DNS service by adding the following `addonFeatures` section after the `fabricSettings` section as shown in the following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="691cc-117">Depois de atualizar o modelo de cluster com as alterações anteriores, aplique-as e permita a conclusão da atualização.</span><span class="sxs-lookup"><span data-stu-id="691cc-117">Once you have updated your cluster template with the preceding changes, apply them and let the upgrade complete.</span></span> <span data-ttu-id="691cc-118">Depois de concluído, o serviço do sistema DNS em execução no cluster, que é chamado de `fabric:/System/DnsService` na seção de serviço do sistema no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="691cc-118">Once complete, the DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in the Service Fabric explorer.</span></span> 

<span data-ttu-id="691cc-119">Como alternativa, você pode habilitar o serviço do DNS por meio do portal no momento da criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="691cc-119">Alternatively, you can enable the DNS service through the portal at the time of cluster creation.</span></span> <span data-ttu-id="691cc-120">O serviço DNS pode ser habilitado pela marcação da caixa de `Include DNS service` no menu `Cluster configuration` conforme mostrado na seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="691cc-120">The DNS service can be enabled by checking the box for `Include DNS service` in the `Cluster configuration` menu as shown in the following screenshot:</span></span>

![Habilitar o serviço DNS por meio do portal][2]


## <a name="setting-the-dns-name-for-your-service"></a><span data-ttu-id="691cc-122">Configurando o nome DNS para o serviço</span><span class="sxs-lookup"><span data-stu-id="691cc-122">Setting the DNS name for your service</span></span>
<span data-ttu-id="691cc-123">Assim que o serviço DNS estiver em execução no cluster, você pode definir um nome DNS para os serviços de forma declarativa para serviços padrão no `ApplicationManifest.xml` ou por meio de comandos do Powershell.</span><span class="sxs-lookup"><span data-stu-id="691cc-123">Once the DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in the `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-the-dns-name-for-a-default-service-in-the-applicationmanifestxml"></a><span data-ttu-id="691cc-124">Definindo o nome DNS de um serviço padrão no ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="691cc-124">Setting the DNS name for a default service in the ApplicationManifest.xml</span></span>
<span data-ttu-id="691cc-125">Abra o projeto no Visual Studio ou em seu editor favorito e abra o arquivo `ApplicationManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="691cc-125">Open your project in Visual Studio, or your favorite editor, and open the `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="691cc-126">Acesse a seção de serviços padrão e, para cada serviço, adicione o atributo `ServiceDnsName`.</span><span class="sxs-lookup"><span data-stu-id="691cc-126">Go to the default services section, and for each service add the `ServiceDnsName` attribute.</span></span> <span data-ttu-id="691cc-127">O exemplo a seguir mostra como definir o nome DNS do serviço como `service1.application1`</span><span class="sxs-lookup"><span data-stu-id="691cc-127">The following example shows how to set the DNS name of the service to `service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="691cc-128">Depois que o aplicativo for implantado, a instância de serviço no Service Fabric Explorer mostrará o nome DNS dessa instância, conforme mostrado na figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="691cc-128">Once the application is deployed, the service instance in the Service Fabric explorer shows the DNS name for this instance, as shown in the following figure:</span></span> 

![pontos de extremidade de serviço][1]

### <a name="setting-the-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="691cc-130">Configurando o nome DNS de um serviço usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="691cc-130">Setting the DNS name for a service using Powershell</span></span>
<span data-ttu-id="691cc-131">Defina o nome DNS de um serviço ao criá-lo usando o `New-ServiceFabricService` PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691cc-131">You can set the DNS name for a service when creating it using the `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="691cc-132">O exemplo a seguir cria um novo serviço sem estado com o nome DNS `service1.application1`</span><span class="sxs-lookup"><span data-stu-id="691cc-132">The following example creates a new stateless service with the DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="691cc-133">Usando o DNS nos serviços</span><span class="sxs-lookup"><span data-stu-id="691cc-133">Using DNS in your services</span></span>
<span data-ttu-id="691cc-134">Se você implantar mais de um serviço, poderá encontrar os pontos de extremidade de outros serviços com os quais se comunicar usando um nome DNS.</span><span class="sxs-lookup"><span data-stu-id="691cc-134">If you deploy more than one service, you can find the endpoints of other services to communicate with  by using a DNS name.</span></span> <span data-ttu-id="691cc-135">O serviço DNS só é aplicável aos serviços sem monitoração de estado, já que o protocolo DNS não pode se comunicar com os serviços com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="691cc-135">The DNS service is only applicable to stateless services, since the DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="691cc-136">Para serviços com estado, use o proxy reverso interno para chamadas HTTP para chamar uma partição de serviço específica.</span><span class="sxs-lookup"><span data-stu-id="691cc-136">For stateful services, you can use the built-in reverse proxy for http calls to call a particular service partition.</span></span>

<span data-ttu-id="691cc-137">O código a seguir mostra como chamar outro serviço, que é simplesmente uma chamada http regular onde você pode fornecer a porta e qualquer caminho opcional como parte da URL.</span><span class="sxs-lookup"><span data-stu-id="691cc-137">The following code shows how to call another service, which is simply a regular http call where you provide the port and any optional path as part of the URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="691cc-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="691cc-138">Next steps</span></span>
<span data-ttu-id="691cc-139">Saiba mais sobre a comunicação de serviço no cluster com [Conectar e comunicar-se com serviços](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="691cc-139">Learn more about service communication within the cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
