---
title: "aaaConfigure o cluster do Azure Service Fabric autônomo | Microsoft Docs"
description: "Saiba como tooconfigure seu autônomo ou cluster do Service Fabric particular."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Definições de configuração para o cluster autônomo no Windows
Este artigo descreve como tooconfigure um cluster de malha do serviço autônomo usando Olá ***Clusterconfig*** arquivo. Você pode usar essas informações de toospecify de arquivo, como nós do Service Fabric hello e seus endereços IP, tipos diferentes de nós no cluster hello, as configurações de segurança hello, bem como topologia de rede de saudação em termos de domínios de falha/atualização, para o seu autônomo cluster.

Quando você [baixar Olá autônomo do Service Fabric pacote](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), alguns exemplos de arquivo de Clusterconfig Olá são baixados tooyour trabalho máquina. exemplos de saudação tendo *DevCluster* em seus nomes ajuda a criar um cluster com todos os três nós no mesmo computador, como nós de lógicas de saudação. Fora isso, pelo menos um nó deve ser marcado como um nó principal. Este cluster é útil para um ambiente de desenvolvimento ou de teste, e não tem suporte como um cluster de produção. exemplos de saudação tendo *MultiMachine* em seus nomes, ajuda a criar um cluster de qualidade de produção, com cada nó em um computador separado.

1. *ClusterConfig.Unsecure.DevCluster.JSON* e *ClusterConfig.Unsecure.MultiMachine.JSON* mostram como toocreate um seguro teste ou produção do cluster respectivamente. 
2. *ClusterConfig.Windows.DevCluster.JSON* e *ClusterConfig.Windows.MultiMachine.JSON* mostrar como cluster de teste ou produção toocreate, protegida usando [a segurança do Windows](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* e *ClusterConfig.X509.MultiMachine.JSON* mostrar como cluster de teste ou produção toocreate, protegida usando [X509 segurança baseada em certificado](service-fabric-windows-cluster-x509-security.md). 

Agora vamos examinar Olá várias seções de um ***Clusterconfig*** arquivo como abaixo.

## <a name="general-cluster-configurations"></a>Configurações gerais do cluster
Isso inclui configurações específicas do hello amplo de cluster, conforme mostrado no trecho JSON a saudação abaixo.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

Você pode fornecer qualquer cluster do nome amigável tooyour Service Fabric atribuindo a ele toohello **nome** variável. Olá **clusterConfigurationVersion** é o número de versão de saudação do cluster; aumentá-lo toda vez que você atualizar seu cluster do Service Fabric. No entanto, você deve deixar Olá **apiVersion** toohello valor de padrão.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Nós no cluster Olá
Você pode configurar nós de saudação no cluster do Service Fabric usando Olá **nós** seção, como Olá trecho a seguir mostra.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Um cluster do Service Fabric deve conter pelo menos 3 nós. Você pode adicionar mais uma seção toothis nós de acordo com a sua instalação. Olá a tabela a seguir explica as definições de configuração de saudação para cada nó.

| **Configuração de nó** | **Descrição** |
| --- | --- |
| nodeName |Você pode fornecer qualquer nó de toohello nome amigável. |
| iPAddress |Descobrir o endereço IP de saudação do nó abrindo uma janela de comando e digitando `ipconfig`. Observe o endereço IPV4 de saudação e atribuí-la toohello **iPAddress** variável. |
| nodeTypeRef |Cada nó pode ser receber um tipo de nó diferente. Olá [tipos de nós](#nodetypes) estão definidos na seção de saudação abaixo. |
| faultDomain |Falha domínios Habilitar administradores toodefine Olá físico nós de cluster que podem falhar em Olá a mesma hora devido a dependências físico tooshared. |
| upgradeDomain |Domínios de atualização descrevem os conjuntos de nós que são encerrados para Service Fabric atualiza cada sobre Olá mesmo tempo. Você pode escolher quais toowhich tooassign de nós domínios de atualização, pois eles não são limitados por quaisquer requisitos físicos. |

## <a name="cluster-properties"></a>Propriedades do cluster
Olá **propriedades** seção Olá Clusterconfig é cluster de saudação tooconfigure usado da seguinte maneira.

<a id="reliability"></a>

### <a name="reliability"></a>Confiabilidade
conceito de saudação do **reliabilityLevel** define o número Olá de réplicas ou instâncias de saudação do Service Fabric dos serviços do sistema que podem ser executados em nós primários de saudação do cluster de saudação. Ele determina a confiabilidade de saudação desses serviços e hello, portanto, o cluster. valor de saudação é calculada pelo sistema Olá em tempo de criação e atualização de cluster.

### <a name="diagnostics"></a>Diagnostics
Olá **diagnosticsStore** seção permite que você tooconfigure diagnóstico de tooenable de parâmetros e nó de solução de problemas ou falhas de cluster, conforme mostrado no hello trecho de código a seguir. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Olá **metadados** é uma descrição do que o diagnóstico do cluster e pode ser definido de acordo com a sua instalação. Essas variáveis ajudam na coleta de logs de rastreamento ETW, despejos de memória e contadores de desempenho. Leia [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) e [Rastreamento ETW](https://msdn.microsoft.com/library/ms751538.aspx) para saber mais sobre os logs de rastreamento de ETW. Todos os logs, inclusive [despejos de memória](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) e [contadores de desempenho](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) pode ser direcionado toohello **connectionString** pasta no seu computador. Você também pode usar *AzureStorage* para o armazenamento de diagnóstico. Veja abaixo um exemplo de trecho de código.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Segurança
Olá **segurança** seção é necessária para um cluster do Service Fabric autônomo segura. saudação de trecho de código a seguir mostra uma parte desta seção.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Olá **metadados** é uma descrição do cluster seguro e pode ser definido de acordo com a sua instalação. Olá **ClusterCredentialType** e **ServerCredentialType** determinar o tipo de saudação de segurança que o cluster hello e nós Olá implementar. Eles podem ser definidos tooeither *X509* para segurança baseada em certificado, ou *Windows* para uma segurança baseada no Active Directory do Azure. Olá restante da saudação **segurança** seção se baseará no tipo de saudação de segurança de saudação. Leitura [segurança baseada em certificados em um cluster autônomo](service-fabric-windows-cluster-x509-security.md) ou [a segurança do Windows em um cluster autônomo](service-fabric-windows-cluster-windows-security.md) para obter informações sobre como toofill out Olá restante da saudação **segurança**seção.

<a id="nodetypes"></a>

### <a name="node-types"></a>Tipos de nó
Olá **nodeTypes** seção descreve o tipo de saudação de nós de saudação que seu cluster tem. Pelo menos um tipo de nó deve ser especificado para um cluster, conforme mostrado no trecho de saudação abaixo. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

Olá **nome** é Olá o nome amigável para este tipo de nó específico. toocreate um nó do tipo de nó, atribuir o nome amigável toohello **nodeTypeRef** variável para esse nó, conforme mencionado [acima](#clusternodes). Para cada tipo de nó, defina pontos de extremidade de conexão de saudação que serão usados. Você pode escolher qualquer número de porta para esses pontos de extremidade de conexão, desde que eles não entrem em conflito com qualquer outro ponto de extremidade neste cluster. Em um cluster de vários nó, haverá um ou mais nós primários (ou seja, **isPrimary** definido muito*true*), dependendo da saudação [ **reliabilityLevel** ](#reliability). Leitura [considerações de planejamento de capacidade de cluster do Service Fabric](service-fabric-cluster-capacity.md) para obter informações sobre **nodeTypes** e **reliabilityLevel**e tooknow quais são principal e Olá tipos de nó não primário. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>Pontos de extremidade usados tipos de nós de saudação tooconfigure
* *clientConnectionEndpointPort* é Olá porta usada pelo Olá cliente tooconnect toohello cluster, ao usar APIs de cliente hello. 
* *clusterConnectionEndpointPort* Olá porta em que nós de saudação se comunicam entre si.
* *leaseDriverEndpointPort* Olá porta usada pelo Olá cluster concessão driver toofind out se nós Olá ainda estão ativas. 
* *serviceConnectionEndpointPort* é a porta Olá usados por aplicativos de saudação e serviços implantados em um nó, toocommunicate com o cliente do Service Fabric Olá naquele nó específico.
* *httpGatewayEndpointPort* Olá porta usados pelo Olá Service Fabric Explorer tooconnect toohello cluster.
* *ephemeralPorts* substituir Olá [portas dinâmicas usadas pelo Olá OS](https://support.microsoft.com/kb/929851). Service Fabric usará uma parte dessas portas do aplicativo e Olá restantes estarão disponíveis para Olá sistema operacional. Ele também mapeará esse intervalo toohello intervalo existente presente no hello sistema operacional, então para todas as finalidades, você pode usar intervalos de saudação fornecidos nos arquivos de JSON de exemplo hello. Você precisa toomake-se de que a diferença Olá entre o início Olá Olá portas e end pelo menos 255. Você pode executar em conflitos se essa diferença é muito baixa, pois esse intervalo é compartilhado com o sistema operacional de saudação. Consulte o intervalo de portas dinâmicas de saudação configurado executando `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* Olá portas que serão usados por aplicativos do Service Fabric hello. intervalo de portas de aplicativo Hello deve ser um requisito de ponto de extremidade de saudação toocover grande o suficiente de seus aplicativos. Esse intervalo deve ser exclusivo no intervalo de porta dinâmica Olá na máquina hello, ou seja, a saudação de *ephemeralPorts* intervalo conforme definido na configuração de saudação.  Malha do serviço será usá-los sempre que novas portas são necessárias, bem como o cuidam de abrir o firewall Olá para essas portas. 
* *reverseProxyEndpointPort* é um ponto de extremidade de proxy reverso opcional. Consulte [Reverter Proxy do Service Fabric](service-fabric-reverseproxy.md) para obter mais detalhes. 

### <a name="log-settings"></a>Configurações de log
Olá **fabricSettings** seção permite que você tooset Olá raiz diretórios Olá Service Fabric dados e logs. Você pode personalizar esses somente durante a criação de cluster inicial de saudação. Veja abaixo um exemplo de trecho de código desta seção.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

É recomendável usando uma unidade não-OS como Olá FabricDataRoot e FabricLogRoot, pois ele oferece mais confiabilidade contra falhas do sistema operacional. Observe que se você personalizar somente raiz de dados hello, em seguida, raiz de log Olá será colocado um nível abaixo da raiz de dados hello.

### <a name="stateful-reliable-service-settings"></a>Configurações de Reliable Service com estado
Olá **KtlLogger** seção permite que você tooset Olá configurações globais para serviços confiáveis. Para obter mais detalhes sobre essas configurações, leia [Configurar o Reliable Services com estado](service-fabric-reliable-services-configuration.md).
exemplo Hello abaixo mostra como toochange Olá Olá compartilhado log de transações que obtém criados tooback todas as coleções confiáveis para serviços com monitoração de estado.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Recursos de complemento
recursos de complemento tooconfigure, Olá apiVersion deve ser configurado como ' 04-2017' ou superior e addonFeatures precisa toobe configurado:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Suporte a contêiner
tooenable suporte de contêiner para o contêiner do windows server e o contêiner do hyper-v para clusters autônomos, recurso de complemento 'DnsService' hello precisa toobe habilitado.


## <a name="next-steps"></a>Próximas etapas
Uma vez que um arquivo Clusterconfig completo configurado de acordo com a configuração de cluster autônomo, você pode implantar o cluster usando o seguinte artigo Olá [criar um cluster do Service Fabric autônomo](service-fabric-cluster-creation-for-windows-server.md) e prossiga muito[visualizar seu cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

