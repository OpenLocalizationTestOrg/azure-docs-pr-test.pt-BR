---
title: "Configurar o cluster do Azure Service Fabric autônomo | Microsoft Docs"
description: "Aprenda a configurar seu cluster autônomo ou particular do Service Fabric."
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
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="c79ce-103">Definições de configuração para o cluster autônomo no Windows</span><span class="sxs-lookup"><span data-stu-id="c79ce-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="c79ce-104">Este artigo descreve como configurar um cluster autônomo do Service Fabric usando o arquivo ***ClusterConfig.JSON***.</span><span class="sxs-lookup"><span data-stu-id="c79ce-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="c79ce-105">Use esse arquivo para especificar informações, como os nós do Service Fabric e seus endereços IP, tipos diferentes de nós no cluster, configurações de segurança, bem como a topologia da rede em termos de domínios de falha/atualização, para o cluster autônomo.</span><span class="sxs-lookup"><span data-stu-id="c79ce-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="c79ce-106">Quando você [baixa o pacote do Service Fabric autônomo](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), alguns exemplos do arquivo ClusterConfig.JSON são baixados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c79ce-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span></span> <span data-ttu-id="c79ce-107">Os exemplos com *DevCluster* em seus nomes ajudarão a criar um cluster com todos os três nós no mesmo computador, como nós lógicos.</span><span class="sxs-lookup"><span data-stu-id="c79ce-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span></span> <span data-ttu-id="c79ce-108">Fora isso, pelo menos um nó deve ser marcado como um nó principal.</span><span class="sxs-lookup"><span data-stu-id="c79ce-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="c79ce-109">Este cluster é útil para um ambiente de desenvolvimento ou de teste, e não tem suporte como um cluster de produção.</span><span class="sxs-lookup"><span data-stu-id="c79ce-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="c79ce-110">Os exemplos com *MultiMachine* em seus nomes ajudarão a criar um cluster de qualidade de produção, com cada nó em um computador separado.</span><span class="sxs-lookup"><span data-stu-id="c79ce-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="c79ce-111">*ClusterConfig.Unsecure.DevCluster.JSON* e *ClusterConfig.Unsecure.MultiMachine.JSON* mostram como criar um cluster de teste ou de produção sem segurança, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c79ce-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="c79ce-112">*ClusterConfig.Windows.DevCluster.JSON* e *ClusterConfig.Windows.MultiMachine.JSON* mostram como criar um cluster de teste ou de produção protegido usando a [segurança do Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="c79ce-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="c79ce-113">*ClusterConfig.X509.DevCluster.JSON* e *ClusterConfig.X509.MultiMachine.JSON* mostram como criar um cluster de teste ou de produção protegido usando a [segurança baseada no certificado X509](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="c79ce-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="c79ce-114">Agora, vamos examinar as várias seções de um arquivo ***ClusterConfig.JSON*** conforme mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="c79ce-114">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="c79ce-115">Configurações gerais do cluster</span><span class="sxs-lookup"><span data-stu-id="c79ce-115">General cluster configurations</span></span>
<span data-ttu-id="c79ce-116">Isso abrange as configurações específicas mais amplas do cluster, conforme mostra o trecho de JSON abaixo.</span><span class="sxs-lookup"><span data-stu-id="c79ce-116">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="c79ce-117">Você pode atribuir qualquer nome amigável ao cluster do Service Fabric, atribuindo a ele a variável **name** .</span><span class="sxs-lookup"><span data-stu-id="c79ce-117">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span></span> <span data-ttu-id="c79ce-118">O **clusterConfigurationVersion** é o número de versão do cluster; você deve aumentá-lo toda vez que atualizar seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c79ce-118">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="c79ce-119">No entanto, deixe a **apiVersion** com o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="c79ce-119">You should however leave the **apiVersion** to the default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="c79ce-120">Nós no cluster</span><span class="sxs-lookup"><span data-stu-id="c79ce-120">Nodes on the cluster</span></span>
<span data-ttu-id="c79ce-121">Você pode configurar os nós no cluster de seu Service Fabric usando a seção **nós** , como mostra o trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="c79ce-121">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span></span>

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

<span data-ttu-id="c79ce-122">Um cluster do Service Fabric deve conter pelo menos 3 nós.</span><span class="sxs-lookup"><span data-stu-id="c79ce-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="c79ce-123">Você pode adicionar mais nós a esta seção de acordo com a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="c79ce-123">You can add more nodes to this section as per your setup.</span></span> <span data-ttu-id="c79ce-124">A tabela a seguir explica as definições de configuração para cada nó.</span><span class="sxs-lookup"><span data-stu-id="c79ce-124">The following table explains the configuration settings for each node.</span></span>

| <span data-ttu-id="c79ce-125">**Configuração de nó**</span><span class="sxs-lookup"><span data-stu-id="c79ce-125">**Node configuration**</span></span> | <span data-ttu-id="c79ce-126">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="c79ce-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c79ce-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="c79ce-127">nodeName</span></span> |<span data-ttu-id="c79ce-128">Você pode atribuir qualquer nome amigável ao nó.</span><span class="sxs-lookup"><span data-stu-id="c79ce-128">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="c79ce-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="c79ce-129">iPAddress</span></span> |<span data-ttu-id="c79ce-130">Descubra o endereço IP do seu nó abrindo uma janela de comando e digitando `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="c79ce-130">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="c79ce-131">Anote o endereço IPV4 e atribua a ele a variável **iPAddress** .</span><span class="sxs-lookup"><span data-stu-id="c79ce-131">Note the IPV4 address and assign it to the **iPAddress** variable.</span></span> |
| <span data-ttu-id="c79ce-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="c79ce-132">nodeTypeRef</span></span> |<span data-ttu-id="c79ce-133">Cada nó pode ser receber um tipo de nó diferente.</span><span class="sxs-lookup"><span data-stu-id="c79ce-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="c79ce-134">Os [tipos de nó](#nodetypes) são definidos na seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="c79ce-134">The [node types](#nodetypes) are defined in the section below.</span></span> |
| <span data-ttu-id="c79ce-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="c79ce-135">faultDomain</span></span> |<span data-ttu-id="c79ce-136">Os domínios de falha permitem que os administradores de cluster definam os nós físicos que podem falhar ao mesmo tempo devido às dependências físicas compartilhadas.</span><span class="sxs-lookup"><span data-stu-id="c79ce-136">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="c79ce-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="c79ce-137">upgradeDomain</span></span> |<span data-ttu-id="c79ce-138">Os domínios de atualização descrevem conjuntos de nós que são desligados para atualizações do Service Fabric quase ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="c79ce-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="c79ce-139">Você pode escolher quais nós atribuir a quais Domínios de atualização, pois eles não são limitados por quaisquer requisitos físicos.</span><span class="sxs-lookup"><span data-stu-id="c79ce-139">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="c79ce-140">Propriedades do cluster</span><span class="sxs-lookup"><span data-stu-id="c79ce-140">Cluster properties</span></span>
<span data-ttu-id="c79ce-141">A seção **propriedades** no ClusterConfig.JSON é usada para configurar o cluster da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="c79ce-141">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="c79ce-142">Confiabilidade</span><span class="sxs-lookup"><span data-stu-id="c79ce-142">Reliability</span></span>
<span data-ttu-id="c79ce-143">O conceito de **reliabilityLevel** define o número de réplicas ou as instâncias dos serviços de sistema do Service Fabric que podem ser executados em nós do cluster primários.</span><span class="sxs-lookup"><span data-stu-id="c79ce-143">The concept of **reliabilityLevel** defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="c79ce-144">Determina a confiabilidade desses serviços e, portanto, do cluster.</span><span class="sxs-lookup"><span data-stu-id="c79ce-144">It determines the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="c79ce-145">O valor é calculado pelo sistema em tempo de criação e atualização de cluster.</span><span class="sxs-lookup"><span data-stu-id="c79ce-145">The value is calcuated by the system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="c79ce-146">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="c79ce-146">Diagnostics</span></span>
<span data-ttu-id="c79ce-147">A seção **diagnosticsStore** permite configurar parâmetros para habilitar o diagnóstico e solucionar problemas de falhas de nó e do cluster, conforme mostra o trecho a seguir.</span><span class="sxs-lookup"><span data-stu-id="c79ce-147">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="c79ce-148">Os **metadados** são uma descrição do diagnóstico do cluster e podem ser definidos de acordo com sua configuração.</span><span class="sxs-lookup"><span data-stu-id="c79ce-148">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="c79ce-149">Essas variáveis ajudam na coleta de logs de rastreamento ETW, despejos de memória e contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="c79ce-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="c79ce-150">Leia [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) e [Rastreamento ETW](https://msdn.microsoft.com/library/ms751538.aspx) para saber mais sobre os logs de rastreamento de ETW.</span><span class="sxs-lookup"><span data-stu-id="c79ce-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="c79ce-151">Todos os logs que incluem [Despejos de memória](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) e [contadores de desempenho](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) podem ser direcionados para a pasta **connectionString** em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c79ce-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span></span> <span data-ttu-id="c79ce-152">Você também pode usar *AzureStorage* para o armazenamento de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c79ce-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="c79ce-153">Veja abaixo um exemplo de trecho de código.</span><span class="sxs-lookup"><span data-stu-id="c79ce-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="c79ce-154">Segurança</span><span class="sxs-lookup"><span data-stu-id="c79ce-154">Security</span></span>
<span data-ttu-id="c79ce-155">A seção **segurança** é necessária para um cluster autônomo seguro do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c79ce-155">The **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="c79ce-156">O trecho a seguir mostra uma parte desta seção.</span><span class="sxs-lookup"><span data-stu-id="c79ce-156">The following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="c79ce-157">Os **metadados** são uma descrição de seu cluster seguro e podem ser definidos de acordo com sua configuração.</span><span class="sxs-lookup"><span data-stu-id="c79ce-157">The **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="c79ce-158">O **ClusterCredentialType** e o **ServerCredentialType** determinam o tipo de segurança que o cluster e os nós implementarão.</span><span class="sxs-lookup"><span data-stu-id="c79ce-158">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span></span> <span data-ttu-id="c79ce-159">Eles podem ser definidos como *X509* para segurança baseada em certificados ou como *Windows* para segurança baseada no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c79ce-159">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="c79ce-160">O restante da seção **segurança** será baseado no tipo de segurança.</span><span class="sxs-lookup"><span data-stu-id="c79ce-160">The rest of the **security** section will be based on the type of the security.</span></span> <span data-ttu-id="c79ce-161">Leia [Segurança baseada em certificados em um cluster autônomo](service-fabric-windows-cluster-x509-security.md) ou [Segurança do Windows em um cluster autônomo](service-fabric-windows-cluster-windows-security.md) para saber como preencher o restante da seção de **segurança**.</span><span class="sxs-lookup"><span data-stu-id="c79ce-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="c79ce-162">Tipos de nó</span><span class="sxs-lookup"><span data-stu-id="c79ce-162">Node Types</span></span>
<span data-ttu-id="c79ce-163">A seção **nodeTypes** descreve o tipo de nó que seu cluster tem.</span><span class="sxs-lookup"><span data-stu-id="c79ce-163">The **nodeTypes** section describes the type of the nodes that your cluster has.</span></span> <span data-ttu-id="c79ce-164">Pelo menos um tipo de nó deve ser especificado para um cluster, como mostrado no fragmento a seguir.</span><span class="sxs-lookup"><span data-stu-id="c79ce-164">At least one node type must be specified for a cluster, as shown in the snippet below.</span></span> 

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

<span data-ttu-id="c79ce-165">O **nome** é o nome amigável para esse tipo de nó específico.</span><span class="sxs-lookup"><span data-stu-id="c79ce-165">The **name** is the friendly name for this particular node type.</span></span> <span data-ttu-id="c79ce-166">Para criar um nó desse tipo, atribua o nome amigável à variável **nodeTypeRef** para esse nó, conforme mencionado [acima](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="c79ce-166">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="c79ce-167">Para cada tipo de nó, defina os pontos de extremidade de conexão que serão usados.</span><span class="sxs-lookup"><span data-stu-id="c79ce-167">For each node type, define the connection endpoints that will be used.</span></span> <span data-ttu-id="c79ce-168">Você pode escolher qualquer número de porta para esses pontos de extremidade de conexão, desde que eles não entrem em conflito com qualquer outro ponto de extremidade neste cluster.</span><span class="sxs-lookup"><span data-stu-id="c79ce-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="c79ce-169">Em um cluster de vários nós, haverá um ou mais nós primários (ou seja, **isPrimary** definido como *true*), dependendo do [**reliabilityLevel**](#reliability).</span><span class="sxs-lookup"><span data-stu-id="c79ce-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="c79ce-170">Leia [Considerações de planejamento de capacidade de cluster do Service Fabric](service-fabric-cluster-capacity.md) para obter informações sobre **nodeTypes** e **reliabilityLevel**, bem como para saber quais são os tipos de nó primários e não primários.</span><span class="sxs-lookup"><span data-stu-id="c79ce-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and to know what are primary and the non-primary node types.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="c79ce-171">Pontos de extremidade usados para configurar os tipos de nó</span><span class="sxs-lookup"><span data-stu-id="c79ce-171">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="c79ce-172">*clientConnectionEndpointPort* é a porta usada pelo cliente para se conectar ao cluster, ao usar as APIs de cliente.</span><span class="sxs-lookup"><span data-stu-id="c79ce-172">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span></span> 
* <span data-ttu-id="c79ce-173">*clusterConnectionEndpointPort* é a porta na qual os nós se comuniquem entre si.</span><span class="sxs-lookup"><span data-stu-id="c79ce-173">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span></span>
* <span data-ttu-id="c79ce-174">*leaseDriverEndpointPort* é a porta usada pelo driver de concessão de cluster para descobrir se os nós ainda estão ativos.</span><span class="sxs-lookup"><span data-stu-id="c79ce-174">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="c79ce-175">*serviceConnectionEndpointPort* é a porta usada pelos aplicativos e serviços implantados em um nó, para se comunicar com o cliente do Service Fabric no nó específico.</span><span class="sxs-lookup"><span data-stu-id="c79ce-175">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="c79ce-176">*httpGatewayEndpointPort* é a porta usada pelo Service Fabric Explorer para se conectar ao cluster.</span><span class="sxs-lookup"><span data-stu-id="c79ce-176">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="c79ce-177">*ephemeralPorts* substituem as [portas dinâmicas usadas pelo sistema operacional](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="c79ce-177">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="c79ce-178">O Service Fabric usará parte dessas portas como portas do aplicativo e o restante estará disponível para o SO.</span><span class="sxs-lookup"><span data-stu-id="c79ce-178">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span></span> <span data-ttu-id="c79ce-179">Ele também mapeará esse intervalo para o intervalo existente presente no SO. Então, para todas as finalidades, você pode usar os intervalos fornecidos nos arquivos JSON de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c79ce-179">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="c79ce-180">Você precisa certificar-se de que a diferença entre as portas de início e de fim é pelo menos 255.</span><span class="sxs-lookup"><span data-stu-id="c79ce-180">You need to make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="c79ce-181">Você poderá encontrar conflitos se a diferença for muito baixa, uma vez que esse intervalo é compartilhado com o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="c79ce-181">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span></span> <span data-ttu-id="c79ce-182">Veja o intervalo de portas dinâmicas configurado executando `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="c79ce-182">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="c79ce-183">*applicationPorts* são portas que serão usadas pelos aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c79ce-183">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span></span> <span data-ttu-id="c79ce-184">O intervalo de portas do aplicativo deve ser amplo o bastante para cobrir o requisito de ponto de extremidade dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c79ce-184">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="c79ce-185">Esse intervalo deve ser exclusivo no intervalo de portas dinâmico no computador, isto é, o intervalo *ephemeralPorts* conforme definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="c79ce-185">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span></span>  <span data-ttu-id="c79ce-186">O Service Fabric usará essas portas sempre que novas portas forem necessárias, bem como cuidará de abrir o firewall para essas portas.</span><span class="sxs-lookup"><span data-stu-id="c79ce-186">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="c79ce-187">*reverseProxyEndpointPort* é um ponto de extremidade de proxy reverso opcional.</span><span class="sxs-lookup"><span data-stu-id="c79ce-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="c79ce-188">Consulte [Reverter Proxy do Service Fabric](service-fabric-reverseproxy.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="c79ce-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="c79ce-189">Configurações de log</span><span class="sxs-lookup"><span data-stu-id="c79ce-189">Log Settings</span></span>
<span data-ttu-id="c79ce-190">A seção **fabricSettings** permite que você defina os diretórios raiz para os dados e logs do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c79ce-190">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="c79ce-191">Você pode personalizá-los somente durante a criação inicial do cluster.</span><span class="sxs-lookup"><span data-stu-id="c79ce-191">You can customize these only during the initial cluster creation.</span></span> <span data-ttu-id="c79ce-192">Veja abaixo um exemplo de trecho de código desta seção.</span><span class="sxs-lookup"><span data-stu-id="c79ce-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="c79ce-193">Recomendamos usar uma unidade não de SO, como FabricDataRoot e FabricLogRoot, pois isso proporciona mais confiabilidade contra falhas do SO.</span><span class="sxs-lookup"><span data-stu-id="c79ce-193">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="c79ce-194">Observe que se você personalizar somente a raiz dos dados, a raiz do log será colocada um nível abaixo da raiz dos dados.</span><span class="sxs-lookup"><span data-stu-id="c79ce-194">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="c79ce-195">Configurações de Reliable Service com estado</span><span class="sxs-lookup"><span data-stu-id="c79ce-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="c79ce-196">A seção **KtlLogger** permite que você defina as configurações globais dos Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="c79ce-196">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="c79ce-197">Para obter mais detalhes sobre essas configurações, leia [Configurar o Reliable Services com estado](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="c79ce-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="c79ce-198">O exemplo a seguir mostra como alterar o log de transações compartilhado que é criado para dar apoio às coleções confiáveis para serviços com estado.</span><span class="sxs-lookup"><span data-stu-id="c79ce-198">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="c79ce-199">Recursos de complemento</span><span class="sxs-lookup"><span data-stu-id="c79ce-199">Add-on features</span></span>
<span data-ttu-id="c79ce-200">Para configurar recursos de complemento, a apiVersion deve ser configurada como ' 04-2017' ou superior e addonFeatures precisa ser configurado:</span><span class="sxs-lookup"><span data-stu-id="c79ce-200">To configure add-on features, the apiVersion should be configured as '04-2017' or higher, and addonFeatures needs to be configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="c79ce-201">Suporte a contêiner</span><span class="sxs-lookup"><span data-stu-id="c79ce-201">Container support</span></span>
<span data-ttu-id="c79ce-202">Para habilitar o suporte de contêiner para o contêiner do windows server e o contêiner do hyper-v para clusters autônomos, o recurso de complemento 'DnsService' deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="c79ce-202">To enable container support for both windows server container and hyper-v container for standalone clusters, the 'DnsService' add-on feature needs to be enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c79ce-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c79ce-203">Next steps</span></span>
<span data-ttu-id="c79ce-204">Depois de configurar um arquivo ClusterConfig.JSON completo de acordo com a configuração do cluster independente, é possível implantar o cluster seguindo o artigo [Criar e gerenciar um cluster em execução no Windows Server](service-fabric-cluster-creation-for-windows-server.md) e continuando com [Visualizando o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c79ce-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

