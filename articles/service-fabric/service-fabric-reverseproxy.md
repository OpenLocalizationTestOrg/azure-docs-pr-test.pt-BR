---
title: proxy reverso do aaaAzure Service Fabric | Microsoft Docs
description: "Use proxy reverso do Service Fabric para toomicroservices de comunicação dentro e fora cluster de saudação."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Proxy reverso no Azure Service Fabric
proxy reverso de saudação que é criado no Azure Service Fabric endereços microservices no cluster do Service Fabric Olá que expõe pontos de extremidade HTTP.

## <a name="microservices-communication-model"></a>Modelo de comunicação de microsserviços
Microservices na malha do serviço geralmente executado em um subconjunto de máquinas virtuais em cluster hello e pode mover de um tooanother de máquina virtual por vários motivos. Portanto, os pontos de extremidade Olá microservices podem ser alterado dinamicamente. saudação padrão típico toocommunicate toohello microsserviço é a seguinte Olá resolver loop:

1. Resolva o local de serviço Olá inicialmente por meio do serviço de nomeação de saudação.
2. Conecte-se o serviço de toohello.
3. Determinar a causa de saudação de falhas de conexão e resolver o local do serviço Olá novamente quando necessário.

Esse processo geralmente envolve a quebra automática de bibliotecas de comunicação de cliente em um loop de repetição que implementa Olá serviço políticas de resolução e tente novamente.
Para obter mais informações, consulte [Conectar-se a serviços e se comunicar com eles](service-fabric-connect-and-communicate-with-services.md).

### <a name="communicating-by-using-hello-reverse-proxy"></a>A comunicação por proxy reverso Olá
proxy reverso de saudação na malha do serviço é executado em todos os nós Olá cluster hello. Ele executa o processo de resolução de todo o serviço de saudação em nome do cliente e, em seguida, encaminha a solicitação de saudação do cliente. Portanto, os clientes que executam no cluster de saudação podem usar qualquer serviço de destino do lado do cliente HTTP comunicação bibliotecas tootalk toohello usando proxy reverso hello, que é executado localmente no hello mesmo nó.

![Comunicação interna][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Alcançar microservices do cluster de saudação externa
modelo de comunicações externas saudação padrão para microservices é um modelo de aceitação em que cada serviço não pode ser acessado diretamente de clientes externos. [O balanceador de carga do Azure](../load-balancer/load-balancer-overview.md), que é um limite de rede entre microservices e clientes externos, faz a conversão de endereços de rede e externas encaminha solicitações de pontos de extremidade de IP: porta toointernal. toomake clientes de tooexternal acessíveis diretamente do ponto de extremidade do microsserviço, primeiro você deve configurar o balanceador de carga usa tooeach porta tooforward tráfego Olá serviço em cluster hello. Além disso, a maioria dos microservices, especialmente com monitoração de estado microservices, não em tempo real em todos os nós de cluster de saudação. Olá microservices pode mover entre nós de failover. Nesses casos, balanceador de carga efetivamente não é possível determinar o local de saudação do nó de destino de saudação do hello réplicas toowhich encaminhar o tráfego.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Alcançar microservices via proxy reverso de saudação do cluster Olá externa
Em vez de configurar a porta de saudação de um serviço individual no balanceador de carga, você pode configurar apenas Olá porta proxy reverso Olá no balanceador de carga. Essa configuração permite que clientes fora do cluster Olá acessar serviços dentro do cluster hello usando proxy reverso de saudação sem configuração adicional.

![Comunicação externa][0]

> [!WARNING]
> Quando você configura a porta do proxy inverso Olá no balanceador de carga, todos os microservices no cluster Olá que expor um ponto de extremidade HTTP são endereçáveis da fora Olá cluster.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>Formato URI para usar serviços usando o proxy reverso Olá
usos de proxy reverso Olá que uma determinado recurso uniforme identificador (URI) formato tooidentify Olá serviço partição toowhich Olá entrada solicitação deve ser encaminhada:

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **http (s):** proxy reverso Olá pode ser configurado tooaccept HTTP ou o tráfego HTTPS. Para encaminhamento de HTTPS, consulte muito[conectar o serviço seguro tooa com proxy reverso Olá](service-fabric-reverseproxy-configure-secure-communication.md) uma vez que toolisten de configuração de proxy reverso em HTTPS.
* **Nome de domínio totalmente qualificado (FQDN) do cluster | IP interno:** para clientes externos, você pode configurar o proxy reverso Olá para que seja acessível por meio do domínio do cluster hello, como mycluster.eastus.cloudapp.azure.com. Por padrão, o proxy reverso Olá executa em cada nó. Para o tráfego interno, proxy reverso Olá pode ser contatado no host local ou em qualquer nó interno de IP, como 10.0.0.1.
* **Porta:** é porta hello, como 19081, que foi especificada para o proxy inverso hello.
* **ServiceInstanceName:** este é o nome totalmente qualificado de saudação da instância de serviço Olá implantado que você está tentando tooreach sem hello "fabric: /" esquema. Por exemplo, tooreach Olá *fabric: / myapp/myservice/* serviço, você usaria *myapp/myservice*.

    nome de instância de serviço Olá diferencia maiusculas de minúsculas. Usando diferenciam maiusculas de minúsculas para o nome de instância de serviço Olá Olá URL faz Olá solicitações toofail 404 (não encontrado).
* **Caminho de sufixo:** este é o caminho da URL real hello, tais como *myapi/valores/adicionar/3*, para o serviço de saudação que você deseja tooconnect para.
* **PartitionKey:** para um serviço particionado, isso é chave de partição computada de saudação da partição Olá que você deseja tooreach. Observe que isso *não* Olá GUID da ID de partição. Esse parâmetro não é necessário para serviços que usam o esquema de partição singleton hello.
* **PartitionKind:** este é o esquema de partição de serviço hello. Isso pode ser 'Int64Range' ou 'Named'. Esse parâmetro não é necessário para serviços que usam o esquema de partição singleton hello.
* **ListenerName** são pontos de extremidade de saudação do serviço de saudação do formulário de saudação {"Pontos de extremidade": {"Listener1": "Endpoint1", "Listener2": "Endpoint2"...}}. Quando o serviço de saudação expõe vários pontos de extremidade, isso identifica o ponto de extremidade de saudação essa solicitação de cliente Olá deve ser encaminhada. Isso pode ser omitido se serviço Olá tiver somente um ouvinte.
* **TargetReplicaSelector** Especifica como a réplica de destino hello ou instância deve ser selecionada.
  * Quando o serviço de destino Olá for com monitoração de estado, Olá TargetReplicaSelector pode ser uma das seguintes Olá: 'PrimaryReplica', 'RandomSecondaryReplica' ou 'RandomReplica'. Quando esse parâmetro não for especificado, o padrão de saudação é 'PrimaryReplica'.
  * Quando o serviço de destino Olá for sem monitoração de estado, o proxy reverso escolhe uma instância aleatória Olá partição tooforward Olá de solicitação do serviço para.
* **Tempo limite:** Isso especifica o tempo limite de saudação para solicitação HTTP de saudação criada pelo serviço de toohello de proxy reverso Olá em nome de solicitação de saudação do cliente. valor padrão de saudação é 60 segundos. Este é um parâmetro opcional.

### <a name="example-usage"></a>Exemplo de uso
Por exemplo, vamos Olá *fabric: / MyApp/MyService* serviço que abre um ouvinte de HTTP Olá URL a seguir:

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

Estes são recursos de saudação para o serviço de saudação:

* `/index.html`
* `/api/users/<userId>`

Se o serviço Olá usa singleton Olá esquema de particionamento, Olá *PartitionKey* e *PartitionKind* parâmetros de cadeia de caracteres de consulta não são necessários e Olá serviço pode ser acessado por meio do gateway hello como:

* Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* Internamente: `http://localhost:19081/MyApp/MyService`

Se o serviço Olá usa Olá Int64 uniforme esquema de particionamento, Olá *PartitionKey* e *PartitionKind* parâmetros de cadeia de caracteres de consulta devem ser usado tooreach uma partição de serviço hello:

* Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* Internamente: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

recursos Olá tooreach Olá serviço expõe, simplesmente colocar o caminho do recurso Olá após nome do serviço Olá Olá URL:

* Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* Internamente: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

gateway Olá encaminhará, em seguida, a URL do serviço de toohello essas solicitações:

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>Tratamento especial para os serviços de compartilhamento de porta
Gateway de aplicativo do Azure tenta tooresolve um serviço endereço novamente e repita a solicitação de saudação quando um serviço não pode ser alcançado. Isso é o principal benefício do Application Gateway porque o código do cliente não precisa tooimplement sua própria solução de serviço e resolver o loop.

Em geral, quando um serviço não pode ser atingido, a instância do serviço hello ou réplica foi movido tooa outro nó como parte de seu ciclo de vida normal. Quando isso acontece, o Application Gateway pode receber uma rede conexão erro indicando que um ponto de extremidade é que nenhum mais aberto em Olá originalmente resolvido endereço.

No entanto, réplicas ou instâncias de serviço podem compartilhar um processo de host e uma porta quando hospedadas por um servidor Web baseado em http.sys, incluindo:

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [WebListener de Núcleo ASP.NET](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

Nessa situação, é provável que o servidor web hello está disponível no processo do host hello e responder toorequests, mas Olá resolvido instância de serviço ou a réplica não está mais disponível no host de saudação. Nesse caso, gateway Olá receberá uma resposta HTTP 404 de servidor de web hello. Como resultado, um HTTP 404 tem dois significados distintos:

- Caso #1: endereço do serviço hello está correto, mas o recurso Olá Olá usuário solicitado não existe.
- Caso #2: o endereço do serviço hello está incorreto e recurso Olá Olá usuário solicitado pode existir em um nó diferente.

Olá primeiro é um HTTP 404 normal, que é considerada um erro do usuário. No entanto, no caso de segundo hello, Olá usuário solicitar um recurso que existe. Application Gateway foi toolocate não é possível que porque o próprio serviço Olá foi movida. Application Gateway necessidades tooresolve Olá endereço novamente e tente solicitar novamente hello.

Application Gateway, portanto, precisa de um toodistinguish de maneira entre esses dois casos. toomake que distinção, uma dica do servidor de saudação é necessária.

* Por padrão, o Application Gateway assume caso #2 e tentar a solicitação de saudação tooresolve e emitir novamente.
* tooindicate caso &#1; tooApplication Gateway, o serviço de saudação deve retornar Olá cabeçalho de resposta HTTP a seguir:

  `X-ServiceFabric : ResourceNotFound`

Esse cabeçalho de resposta HTTP indica uma situação de HTTP 404 normal no qual Olá recurso solicitado não existe e o Application Gateway não tentará endereço do serviço Olá tooresolve novamente.

## <a name="setup-and-configuration"></a>Instalação e configuração

### <a name="enable-reverse-proxy-via-azure-portal"></a>Habilitar proxy reverso por meio do portal do Azure

Portal do Azure fornece um proxy reverso de tooenable opção ao criar um novo cluster do Service Fabric.
Em **cluster do Service Fabric criar**, etapa 2: configuração de Cluster, configuração do tipo de nó, selecione caixa de seleção de saudação muito "Habilitar proxy reverso".
Para configurar o proxy reverso seguro, o certificado SSL pode ser especificado na etapa 3: segurança, definir configurações de segurança de cluster, Olá selecione caixa de seleção "Incluir um certificado SSL para o proxy inverso" e insira os detalhes do certificado de saudação muito.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Habilitar proxy reverso, por meio de modelos do Azure Resource Manager

Você pode usar o hello [modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable Olá proxy reverso na malha do serviço de cluster hello.

Consulte também[configurar Proxy reverso HTTPS em um cluster seguro](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) para o Azure Resource Manager tooconfigure o proxy reverso seguro com a substituição de certificado do certificado e tratamento de amostras de modelo.

Primeiro, você obterá modelo Olá para cluster Olá que você deseja toodeploy. Você pode usar modelos de exemplo hello ou criar um modelo personalizado do Gerenciador de recursos. Em seguida, você pode habilitar o proxy reverso hello usando Olá etapas a seguir:

1. Definir uma porta de proxy reverso Olá em Olá [seção parâmetros](../azure-resource-manager/resource-group-authoring-templates.md) do modelo de saudação.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. Especifique a porta de saudação para cada um dos objetos de nodetype Olá Olá **Cluster** [seção de tipo de recurso](../azure-resource-manager/resource-group-authoring-templates.md).

    porta de saudação é identificada pelo nome do parâmetro hello, reverseProxyEndpointPort.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. Olá tooaddress proxy reverso da saudação fora cluster do Azure, configurar as regras de Balanceador de carga do Azure Olá para a porta de saudação que você especificou na etapa 1.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. certificados SSL de tooconfigure na porta de saudação de proxy reverso do hello, adicionar Olá certificado toohello ***reverseProxyCertificate*** propriedade Olá **Cluster** [seção de tipo de recurso](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Dando suporte a um certificado de proxy reverso que é diferente do certificado de cluster Olá
 Se o certificado de proxy reverso Olá for diferente do certificado de saudação que protege cluster hello, em seguida, Olá especificado anteriormente certificado deve ser instalado na máquina virtual de saudação e adicionado toohello lista de controle de acesso (ACL) para que possa Service Fabric acessá-lo. Isso pode ser feito no hello **virtualMachineScaleSets** [seção de tipo de recurso](../resource-group-authoring-templates.md). Para a instalação, adicione esse osProfile toohello de certificado. seção de extensões de saudação do modelo de saudação pode atualizar o certificado Olá Olá ACL.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> Quando você usa certificados que são diferentes da saudação cluster certificado tooenable Olá proxy reverso em um cluster existente, instalar certificado de proxy reverso hello e atualizar Olá ACL no cluster de saudação antes de habilitar o proxy reverso hello. Olá completa [modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) implantação usando as configurações de saudação mencionadas anteriormente antes de iniciar um proxy reverso do tooenable Olá de implantação em etapas 1 a 4.

## <a name="next-steps"></a>Próximas etapas
* Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [O serviço HTTP toosecure de encaminhamento com proxy reverso Olá](service-fabric-reverseproxy-configure-secure-communication.md)
* [Comunicação remota de serviço com os Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [API Web que usa o OWIN nos Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicação WCF usando os Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* Para obter outras opções de configuração de proxy reverso, consulte a seção ApplicationGateway/Http em [Personalizar as configurações de cluster do Service Fabric](service-fabric-cluster-fabric-settings.md).

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
