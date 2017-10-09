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
# <a name="dns-service-in-azure-service-fabric"></a>Serviço DNS no Azure Service Fabric
Olá serviço DNS é um serviço de sistema opcional que você pode habilitar no seu cluster toodiscover outros serviços usando o protocolo DNS hello.

Muitos serviços, especialmente em contêineres services, podem ter um nome de URL existente e ser capaz de tooresolve-los usar o protocolo de DNS padrão da saudação (em vez de protocolo de serviço de nomes de saudação) é desejável, particularmente em cenários de "comparar e deslocar". Olá serviço DNS permite que você toomap DNS nomes tooa nome do serviço e, portanto, resolva endereços IP do ponto de extremidade. 

Olá serviço DNS mapeia nomes tooservice nomes DNS, que por sua vez são resolvidos pelo ponto de extremidade do hello Naming Service tooreturn Olá serviço. nome DNS de saudação para serviço de saudação é fornecido no momento de saudação da criação. 

![pontos de extremidade de serviço][0]

## <a name="enabling-hello-dns-service"></a>Habilitar o serviço de DNS Olá
Primeiro você precisa de serviço DNS de Olá tooenable em seu cluster. Obter modelo Olá cluster Olá que você deseja toodeploy. Pode hello ou use [modelos de exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) ou criar um modelo do Gerenciador de recursos. Você pode habilitar o serviço DNS de saudação com hello etapas a seguir:

1. Verifique que Olá `apiversion` está definido muito`2017-07-01-preview` para Olá `Microsoft.ServiceFabric/clusters` recursos e se não, atualizá-lo conforme Olá trecho de código a seguir:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Agora ativar o serviço DNS de saudação adicionando Olá seguintes `addonFeatures` seção após Olá `fabricSettings` seção conforme Olá trecho de código a seguir: 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. Depois de atualizar o modelo de cluster com hello anterior alterações, aplicá-los e permitem Olá atualização concluída. Uma vez concluído, Olá serviço de sistema DNS começa a ser executado no cluster que é chamado `fabric:/System/DnsService` na seção de serviço do sistema no Gerenciador do Service Fabric hello. 

Como alternativa, você pode habilitar Olá serviço DNS por meio do portal Olá em tempo de saudação da criação do cluster. Olá serviço DNS pode ser habilitado, marcando a caixa de saudação `Include DNS service` em Olá `Cluster configuration` menu conforme Olá captura de tela a seguir:

![Habilitar o serviço do DNS por meio do portal Olá][2]


## <a name="setting-hello-dns-name-for-your-service"></a>Configurar nome DNS de saudação para seu serviço
Quando Olá serviço DNS estiver em execução no cluster, você pode definir um nome DNS para seus serviços declarativamente para serviços padrão em Olá `ApplicationManifest.xml` ou por meio de comandos do Powershell.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Nome DNS de saudação para um serviço padrão da configuração na Olá ApplicationManifest.xml
Abra seu projeto no Visual Studio ou seu editor favorito e Olá `ApplicationManifest.xml` arquivo. Vá toohello seção de serviços padrão e para cada saudação de adicionar serviço `ServiceDnsName` atributo. saudação de exemplo a seguir mostra como tooset Olá nome DNS do serviço de saudação muito`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Depois que o aplicativo hello é implantado, instância de serviço de saudação no hello Service Fabric explorer mostra nome DNS de saudação nessa instância, conforme mostrado na figura a seguir de saudação: 

![pontos de extremidade de serviço][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Configurar nome DNS de saudação para um serviço usando o Powershell
Você pode definir o nome DNS de saudação para um serviço ao criá-la usando Olá `New-ServiceFabricService` Powershell. Olá exemplo a seguir cria um novo serviço sem monitoração de estado com o nome DNS Olá`service1.application1`

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

## <a name="using-dns-in-your-services"></a>Usando o DNS nos serviços
Se você implantar mais de um serviço, você pode encontrar pontos de extremidade de saudação do toocommunicate outros serviços com usando um nome DNS. Olá serviço DNS só é aplicável toostateless serviços, como Olá protocolo DNS não pode se comunicar com os serviços com monitoração de estado. Para serviços com monitoração de estado, você pode usar o proxy reverso internos de saudação para http chamadas toocall uma partição de serviço específico.

Olá código a seguir mostra como toocall outro serviço, que é simplesmente um http regular chamar onde você pode fornecer a porta de saudação e qualquer caminho opcional como parte da URL de saudação.

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

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre a comunicação de serviço em cluster Olá com [se conectar e se comunicar com serviços](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
