---
title: "Configurar o cluster do Azure Service Fabric autônomo | Microsoft Docs"
description: "Aprenda a configurar seu cluster autônomo ou local do Azure Service Fabric."
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
ms.date: 12/06/2017
ms.author: dekapur
ms.openlocfilehash: bd6e5c1591d01329d95ccb168e5a14e436920baf
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2017
---
# <a name="configuration-settings-for-a-standalone-windows-cluster"></a>Definições de configuração para um cluster autônomo no Windows
Este artigo descreve como configurar um cluster autônomo do Microsoft Azure Service Fabric utilizando o arquivo ClusterConfig.json. Este arquivo será utilizado para especificar informações sobre os nós do cluster, as configurações de segurança, assim como a topologia de rede em termos de domínio de atualização e falha.

Ao [fazer o download do pacote do Service Fabric autônomo](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), os exemplos ClusterConfig.json também são incluídos. As exemplos com "DevCluster" em seus nomes criam um cluster com os três nós no mesmo computador, utilizando nós lógicos. Desses nós, pelo menos um deve ser marcado como nó principal. Esse tipo de cluster é útil para ambientes de teste ou desenvolvimento. Ele não tem suporte como um cluster de produção. Os exemplos que possuem "MultiMachine" em seus nomes ajudam a criar clusters de nível de produção, com cada nó em um computador separado. O número de nós primários para esses clusters é baseado no [nível de confiabilidade](#reliability) do cluster. Na API versão 5.7 de 05-2017, removemos a propriedade do nível de confiabilidade. Em vez disso, nosso código calcula o nível de confiabilidade mais otimizado para seu cluster. Não tente definir um valor para essa propriedade em versões 5.7 em diante.


* ClusterConfig.Unsecure.DevCluster.json e lusterConfig.Unsecure.MultiMachine.json mostram como criar um cluster de teste ou de produção sem segurança, respectivamente.

* ClusterConfig.Windows.DevCluster.json ClusterConfig.Windows.MultiMachine.json mostram como criar um cluster de teste ou de produção protegido usando a [segurança do Windows](service-fabric-windows-cluster-windows-security.md).

* ClusterConfig.X509.DevCluster.json e ClusterConfig.X509.MultiMachine.json mostram como criar um cluster de teste ou de produção protegido usando a [segurança baseada no certificado X509](service-fabric-windows-cluster-x509-security.md).

Agora, vamos examinar as várias seções de um arquivo ClusterConfig.json.

## <a name="general-cluster-configurations"></a>Configurações gerais do cluster
As configurações de cluster geral abordam as configurações gerais específicas do cluster, conforme mostrado no seguinte trecho JSON:

```json
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",
```

Você pode atribuir qualquer nome amigável ao cluster do Service Fabric, atribuindo a ele a variável name. O clusterConfigurationVersion é o número de versão do cluster. Aumente-o toda vez que você atualizar seu cluster do Service Fabric. Deixe apiVersion com o valor padrão.

## <a name="nodes-on-the-cluster"></a>Nós no cluster

    <a id="clusternodes"></a>

Você pode configurar os nós no cluster de seu Service Fabric usando a seção nodes, como mostra o trecho de código a seguir:

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

Um cluster do Service Fabric deve conter pelo menos três nós. Você pode adicionar mais nós a esta seção de acordo com a sua configuração. A tabela abaixo explica as definições de configuração para cada nó:

| **Configuração de nó** | **Descrição** |
| --- | --- |
| nodeName |Você pode atribuir qualquer nome amigável ao nó. |
| iPAddress |Descubra o endereço IP do seu nó abrindo uma janela de comando e digitando `ipconfig`. Anote o endereço IPV4 e atribua a ele a variável iPAddress. |
| nodeTypeRef |Cada nó pode ser receber um tipo de nó diferente. Os [tipos de nó](#node-types) são definidos na seção a seguir. |
| faultDomain |Os domínios de falha permitem que os administradores de cluster definam os nós físicos que podem falhar ao mesmo tempo devido às dependências físicas compartilhadas. |
| upgradeDomain |Os domínios de atualização descrevem conjuntos de nós que são desligados para atualizações do Service Fabric quase ao mesmo tempo. Você pode escolher quais nós atribuir a quais domínios de atualização, pois eles não são limitados por requisitos físicos. |

## <a name="cluster-properties"></a>Propriedades do cluster
A seção propriedades no ClusterConfig.json é usada para configurar o cluster da seguinte maneira:

### <a name="reliability"></a>Confiabilidade
O conceito de reliabilityLevel define o número de réplicas ou as instâncias dos serviços de sistema do Service Fabric que podem ser executados em nós do cluster primários. Determina a confiabilidade desses serviços e, portanto, do cluster. O valor é calculado pelo sistema na hora da criação e da atualização do cluster.

    <a id="reliability"></a>

### <a name="diagnostics"></a>Diagnostics
Na seção diagnosticsStore, você pode configurar parâmetros para habilitar o diagnóstico e solucionar problemas de falhas de nó e do cluster, conforme mostra o seguinte trecho de código: 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Os metadados são uma descrição do diagnóstico do cluster e podem ser definidos de acordo com sua configuração. Essas variáveis ajudam na coleta de logs de rastreamento ETW e despejos de memória, além de contadores de desempenho. Para saber mais sobre os logs de rastreamento de ETW, leia [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) e [Rastreamento ETW](https://msdn.microsoft.com/library/ms751538.aspx). Todos os logs que incluem [despejos de memória](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) e [contadores de desempenho](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) podem ser direcionados para a pasta connectionString em seu computador. Você também pode usar AzureStorage para armazenar diagnósticos. Consulte o seguinte trecho de código de exemplo:

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Segurança
A seção security é necessária para um cluster autônomo seguro do Service Fabric. O trecho abaixo mostra uma parte desta seção:

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Os metadados são uma descrição de seu cluster seguro e podem ser definidos de acordo com sua configuração. O ClusterCredentialType e o ServerCredentialType determinam o tipo de segurança que o cluster e os nós implementam. Eles podem ser definidos como *X509* para segurança baseada em certificados ou como *Windows* para segurança baseada no Azure Active Directory. O restante da seção segurança se baseia no tipo de segurança. Para saber como preencher o restante da seção de segurança, confira [Segurança baseada em certificados em um cluster autônomo](service-fabric-windows-cluster-x509-security.md) ou [Segurança do Windows em um cluster autônomo](service-fabric-windows-cluster-windows-security.md).

### <a name="node-types"></a>Tipos de nó

    <a id="nodetypes"></a>

A seção nodeTypes descreve o tipo de nó que seu cluster tem. Pelo menos um tipo de nó deve ser especificado para um cluster, como mostrado no seguinte trecho de código: 

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

O nome é o nome amigável para esse tipo de nó específico. Para criar um nó desse tipo, atribua o nome amigável à variável nodeTypeRef para esse nó, [conforme mencionado anteriormente](#nodes-on-the-cluster). Para cada tipo de nó, defina os pontos de extremidade de conexão que serão usados. Você pode escolher qualquer número da porta para esses pontos de extremidade de conexão, desde que eles não entrem em conflito com qualquer outro ponto de extremidade neste cluster. Em um cluster de vários nós, há um ou mais nós primários (ou seja, isPrimary definido como *true*), dependendo do [reliabilityLevel](#reliability). Para saber quais são os tipos de nó primários e não primários, confira [Considerações de planejamento de capacidade de cluster do Service Fabric](service-fabric-cluster-capacity.md) para saber mais sobre nodeTypes e reliabilityLevel. 

#### <a name="endpoints-used-to-configure-the-node-types"></a>Pontos de extremidade usados para configurar os tipos de nó
* clientConnectionEndpointPort é a porta usada pelo cliente para se conectar ao cluster quando as APIs de cliente são usadas. 
* clusterConnectionEndpointPort é a porta na qual os nós se comunicam entre si.
* leaseDriverEndpointPort é a porta usada pelo driver de concessão de cluster para descobrir se os nós ainda estão ativos. 
* serviceConnectionEndpointPort é a porta usada pelos aplicativos e serviços implantados em um nó, para se comunicar com o cliente do Service Fabric no nó específico.
* httpGatewayEndpointPort é a porta usada pelo Service Fabric Explorer para se conectar ao cluster.
* ephemeralPorts substituem as [portas dinâmicas usadas pelo sistema operacional](https://support.microsoft.com/kb/929851). O Service Fabric usa parte dessas portas como portas do aplicativo e o restante fica disponível para o SO. Ele também mapeia esse intervalo para o intervalo existente presente no SO. Então, para todas as finalidades, você pode usar os intervalos fornecidos nos arquivos JSON de exemplo. Verifique se a diferença entre as portas de início e de fim é de pelo menos 255. Você poderá encontrar conflitos se a diferença for muito baixa, uma vez que esse intervalo é compartilhado com o sistema operacional. Para ver o intervalo de portas dinâmicas configurado, execute `netsh int ipv4 show dynamicport tcp`.
* applicationPorts são portas usadas pelos aplicativos do Service Fabric. O intervalo de portas do aplicativo deve ser amplo o bastante para cobrir o requisito de ponto de extremidade dos aplicativos. Esse intervalo deve ser exclusivo no intervalo de portas dinâmico no computador, isto é, o intervalo ephemeralPorts conforme definido na configuração. O Service Fabric usará essas portas sempre que novas portas forem necessárias, e também cuidará de abrir o firewall para essas portas. 
* reverseProxyEndpointPort é um ponto de extremidade de proxy reverso opcional. Para saber mais, confira [proxy inverso do Service Fabric](service-fabric-reverseproxy.md). 

### <a name="log-settings"></a>Configurações de log
Na seção fabricSettings, você pode definir os diretórios raiz para os dados e logs do Service Fabric. Você só pode personalizar esses diretórios durante a criação inicial do cluster. Confira o seguinte trecho de código de exemplo da seção:

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

Recomendamos que você use uma unidade que não seja a do SO, como o FabricDataRoot e o FabricLogRoot. Ela oferece mais confiabilidade para evitar situações de falta de resposta do SO. Se você personalizar somente a raiz dos dados, a raiz do log será colocada um nível abaixo da raiz dos dados.

### <a name="stateful-reliable-services-settings"></a>Configurações de serviço confiável com estado
Na seção KtlLogger, você pode definir as configurações globais dos Reliable Services. Para saber mais sobre essas configurações, confira [Configurar serviços confiáveis com estado](service-fabric-reliable-services-configuration.md). O exemplo abaixo mostra como alterar o log de transações compartilhado que é criado para dar apoio às coleções confiáveis para serviços com estado:

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Recursos de complemento
Para configurar recursos de complemento, configure a apiVersion de abril de 2017 ou mais recente e configure o addonFeatures conforme mostrado aqui:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Suporte a contêiner
Para habilitar o suporte de contêiner para os contêineres do Windows Server e os contêineres do Hyper-V para clusters autônomos, o recurso de complemento DnsService precisa ser habilitado.


## <a name="next-steps"></a>Próximas etapas
Depois de obter um arquivo ClusterConfig.json completo configurado de acordo com a configuração de cluster autônomo, você poderá implantar o cluster. Siga as etapas em [Criar um cluster do Service Fabric autônomo](service-fabric-cluster-creation-for-windows-server.md). Vá para [Visualizar seu cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) e siga as etapas.

