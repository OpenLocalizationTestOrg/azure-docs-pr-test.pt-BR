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
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="3f673-103">Definições de configuração para o cluster autônomo no Windows</span><span class="sxs-lookup"><span data-stu-id="3f673-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="3f673-104">Este artigo descreve como tooconfigure um cluster de malha do serviço autônomo usando Olá ***Clusterconfig*** arquivo.</span><span class="sxs-lookup"><span data-stu-id="3f673-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="3f673-105">Você pode usar essas informações de toospecify de arquivo, como nós do Service Fabric hello e seus endereços IP, tipos diferentes de nós no cluster hello, as configurações de segurança hello, bem como topologia de rede de saudação em termos de domínios de falha/atualização, para o seu autônomo cluster.</span><span class="sxs-lookup"><span data-stu-id="3f673-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="3f673-106">Quando você [baixar Olá autônomo do Service Fabric pacote](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), alguns exemplos de arquivo de Clusterconfig Olá são baixados tooyour trabalho máquina.</span><span class="sxs-lookup"><span data-stu-id="3f673-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="3f673-107">exemplos de saudação tendo *DevCluster* em seus nomes ajuda a criar um cluster com todos os três nós no mesmo computador, como nós de lógicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f673-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="3f673-108">Fora isso, pelo menos um nó deve ser marcado como um nó principal.</span><span class="sxs-lookup"><span data-stu-id="3f673-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="3f673-109">Este cluster é útil para um ambiente de desenvolvimento ou de teste, e não tem suporte como um cluster de produção.</span><span class="sxs-lookup"><span data-stu-id="3f673-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="3f673-110">exemplos de saudação tendo *MultiMachine* em seus nomes, ajuda a criar um cluster de qualidade de produção, com cada nó em um computador separado.</span><span class="sxs-lookup"><span data-stu-id="3f673-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="3f673-111">*ClusterConfig.Unsecure.DevCluster.JSON* e *ClusterConfig.Unsecure.MultiMachine.JSON* mostram como toocreate um seguro teste ou produção do cluster respectivamente.</span><span class="sxs-lookup"><span data-stu-id="3f673-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="3f673-112">*ClusterConfig.Windows.DevCluster.JSON* e *ClusterConfig.Windows.MultiMachine.JSON* mostrar como cluster de teste ou produção toocreate, protegida usando [a segurança do Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="3f673-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="3f673-113">*ClusterConfig.X509.DevCluster.JSON* e *ClusterConfig.X509.MultiMachine.JSON* mostrar como cluster de teste ou produção toocreate, protegida usando [X509 segurança baseada em certificado](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="3f673-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="3f673-114">Agora vamos examinar Olá várias seções de um ***Clusterconfig*** arquivo como abaixo.</span><span class="sxs-lookup"><span data-stu-id="3f673-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="3f673-115">Configurações gerais do cluster</span><span class="sxs-lookup"><span data-stu-id="3f673-115">General cluster configurations</span></span>
<span data-ttu-id="3f673-116">Isso inclui configurações específicas do hello amplo de cluster, conforme mostrado no trecho JSON a saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="3f673-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="3f673-117">Você pode fornecer qualquer cluster do nome amigável tooyour Service Fabric atribuindo a ele toohello **nome** variável.</span><span class="sxs-lookup"><span data-stu-id="3f673-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="3f673-118">Olá **clusterConfigurationVersion** é o número de versão de saudação do cluster; aumentá-lo toda vez que você atualizar seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3f673-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="3f673-119">No entanto, você deve deixar Olá **apiVersion** toohello valor de padrão.</span><span class="sxs-lookup"><span data-stu-id="3f673-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="3f673-120">Nós no cluster Olá</span><span class="sxs-lookup"><span data-stu-id="3f673-120">Nodes on hello cluster</span></span>
<span data-ttu-id="3f673-121">Você pode configurar nós de saudação no cluster do Service Fabric usando Olá **nós** seção, como Olá trecho a seguir mostra.</span><span class="sxs-lookup"><span data-stu-id="3f673-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

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

<span data-ttu-id="3f673-122">Um cluster do Service Fabric deve conter pelo menos 3 nós.</span><span class="sxs-lookup"><span data-stu-id="3f673-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="3f673-123">Você pode adicionar mais uma seção toothis nós de acordo com a sua instalação.</span><span class="sxs-lookup"><span data-stu-id="3f673-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="3f673-124">Olá a tabela a seguir explica as definições de configuração de saudação para cada nó.</span><span class="sxs-lookup"><span data-stu-id="3f673-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="3f673-125">**Configuração de nó**</span><span class="sxs-lookup"><span data-stu-id="3f673-125">**Node configuration**</span></span> | <span data-ttu-id="3f673-126">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="3f673-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="3f673-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="3f673-127">nodeName</span></span> |<span data-ttu-id="3f673-128">Você pode fornecer qualquer nó de toohello nome amigável.</span><span class="sxs-lookup"><span data-stu-id="3f673-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="3f673-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="3f673-129">iPAddress</span></span> |<span data-ttu-id="3f673-130">Descobrir o endereço IP de saudação do nó abrindo uma janela de comando e digitando `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="3f673-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="3f673-131">Observe o endereço IPV4 de saudação e atribuí-la toohello **iPAddress** variável.</span><span class="sxs-lookup"><span data-stu-id="3f673-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="3f673-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="3f673-132">nodeTypeRef</span></span> |<span data-ttu-id="3f673-133">Cada nó pode ser receber um tipo de nó diferente.</span><span class="sxs-lookup"><span data-stu-id="3f673-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="3f673-134">Olá [tipos de nós](#nodetypes) estão definidos na seção de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="3f673-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="3f673-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="3f673-135">faultDomain</span></span> |<span data-ttu-id="3f673-136">Falha domínios Habilitar administradores toodefine Olá físico nós de cluster que podem falhar em Olá a mesma hora devido a dependências físico tooshared.</span><span class="sxs-lookup"><span data-stu-id="3f673-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="3f673-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="3f673-137">upgradeDomain</span></span> |<span data-ttu-id="3f673-138">Domínios de atualização descrevem os conjuntos de nós que são encerrados para Service Fabric atualiza cada sobre Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="3f673-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="3f673-139">Você pode escolher quais toowhich tooassign de nós domínios de atualização, pois eles não são limitados por quaisquer requisitos físicos.</span><span class="sxs-lookup"><span data-stu-id="3f673-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="3f673-140">Propriedades do cluster</span><span class="sxs-lookup"><span data-stu-id="3f673-140">Cluster properties</span></span>
<span data-ttu-id="3f673-141">Olá **propriedades** seção Olá Clusterconfig é cluster de saudação tooconfigure usado da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="3f673-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="3f673-142">Confiabilidade</span><span class="sxs-lookup"><span data-stu-id="3f673-142">Reliability</span></span>
<span data-ttu-id="3f673-143">conceito de saudação do **reliabilityLevel** define o número Olá de réplicas ou instâncias de saudação do Service Fabric dos serviços do sistema que podem ser executados em nós primários de saudação do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f673-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="3f673-144">Ele determina a confiabilidade de saudação desses serviços e hello, portanto, o cluster.</span><span class="sxs-lookup"><span data-stu-id="3f673-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="3f673-145">valor de saudação é calculada pelo sistema Olá em tempo de criação e atualização de cluster.</span><span class="sxs-lookup"><span data-stu-id="3f673-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="3f673-146">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="3f673-146">Diagnostics</span></span>
<span data-ttu-id="3f673-147">Olá **diagnosticsStore** seção permite que você tooconfigure diagnóstico de tooenable de parâmetros e nó de solução de problemas ou falhas de cluster, conforme mostrado no hello trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="3f673-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="3f673-148">Olá **metadados** é uma descrição do que o diagnóstico do cluster e pode ser definido de acordo com a sua instalação.</span><span class="sxs-lookup"><span data-stu-id="3f673-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="3f673-149">Essas variáveis ajudam na coleta de logs de rastreamento ETW, despejos de memória e contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="3f673-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="3f673-150">Leia [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) e [Rastreamento ETW](https://msdn.microsoft.com/library/ms751538.aspx) para saber mais sobre os logs de rastreamento de ETW.</span><span class="sxs-lookup"><span data-stu-id="3f673-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="3f673-151">Todos os logs, inclusive [despejos de memória](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) e [contadores de desempenho](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) pode ser direcionado toohello **connectionString** pasta no seu computador.</span><span class="sxs-lookup"><span data-stu-id="3f673-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="3f673-152">Você também pode usar *AzureStorage* para o armazenamento de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3f673-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="3f673-153">Veja abaixo um exemplo de trecho de código.</span><span class="sxs-lookup"><span data-stu-id="3f673-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="3f673-154">Segurança</span><span class="sxs-lookup"><span data-stu-id="3f673-154">Security</span></span>
<span data-ttu-id="3f673-155">Olá **segurança** seção é necessária para um cluster do Service Fabric autônomo segura.</span><span class="sxs-lookup"><span data-stu-id="3f673-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="3f673-156">saudação de trecho de código a seguir mostra uma parte desta seção.</span><span class="sxs-lookup"><span data-stu-id="3f673-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="3f673-157">Olá **metadados** é uma descrição do cluster seguro e pode ser definido de acordo com a sua instalação.</span><span class="sxs-lookup"><span data-stu-id="3f673-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="3f673-158">Olá **ClusterCredentialType** e **ServerCredentialType** determinar o tipo de saudação de segurança que o cluster hello e nós Olá implementar.</span><span class="sxs-lookup"><span data-stu-id="3f673-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="3f673-159">Eles podem ser definidos tooeither *X509* para segurança baseada em certificado, ou *Windows* para uma segurança baseada no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f673-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="3f673-160">Olá restante da saudação **segurança** seção se baseará no tipo de saudação de segurança de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f673-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="3f673-161">Leitura [segurança baseada em certificados em um cluster autônomo](service-fabric-windows-cluster-x509-security.md) ou [a segurança do Windows em um cluster autônomo](service-fabric-windows-cluster-windows-security.md) para obter informações sobre como toofill out Olá restante da saudação **segurança**seção.</span><span class="sxs-lookup"><span data-stu-id="3f673-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="3f673-162">Tipos de nó</span><span class="sxs-lookup"><span data-stu-id="3f673-162">Node Types</span></span>
<span data-ttu-id="3f673-163">Olá **nodeTypes** seção descreve o tipo de saudação de nós de saudação que seu cluster tem.</span><span class="sxs-lookup"><span data-stu-id="3f673-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="3f673-164">Pelo menos um tipo de nó deve ser especificado para um cluster, conforme mostrado no trecho de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="3f673-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

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

<span data-ttu-id="3f673-165">Olá **nome** é Olá o nome amigável para este tipo de nó específico.</span><span class="sxs-lookup"><span data-stu-id="3f673-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="3f673-166">toocreate um nó do tipo de nó, atribuir o nome amigável toohello **nodeTypeRef** variável para esse nó, conforme mencionado [acima](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="3f673-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="3f673-167">Para cada tipo de nó, defina pontos de extremidade de conexão de saudação que serão usados.</span><span class="sxs-lookup"><span data-stu-id="3f673-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="3f673-168">Você pode escolher qualquer número de porta para esses pontos de extremidade de conexão, desde que eles não entrem em conflito com qualquer outro ponto de extremidade neste cluster.</span><span class="sxs-lookup"><span data-stu-id="3f673-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="3f673-169">Em um cluster de vários nó, haverá um ou mais nós primários (ou seja, **isPrimary** definido muito*true*), dependendo da saudação [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="3f673-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="3f673-170">Leitura [considerações de planejamento de capacidade de cluster do Service Fabric](service-fabric-cluster-capacity.md) para obter informações sobre **nodeTypes** e **reliabilityLevel**e tooknow quais são principal e Olá tipos de nó não primário.</span><span class="sxs-lookup"><span data-stu-id="3f673-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="3f673-171">Pontos de extremidade usados tipos de nós de saudação tooconfigure</span><span class="sxs-lookup"><span data-stu-id="3f673-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="3f673-172">*clientConnectionEndpointPort* é Olá porta usada pelo Olá cliente tooconnect toohello cluster, ao usar APIs de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="3f673-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="3f673-173">*clusterConnectionEndpointPort* Olá porta em que nós de saudação se comunicam entre si.</span><span class="sxs-lookup"><span data-stu-id="3f673-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="3f673-174">*leaseDriverEndpointPort* Olá porta usada pelo Olá cluster concessão driver toofind out se nós Olá ainda estão ativas.</span><span class="sxs-lookup"><span data-stu-id="3f673-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="3f673-175">*serviceConnectionEndpointPort* é a porta Olá usados por aplicativos de saudação e serviços implantados em um nó, toocommunicate com o cliente do Service Fabric Olá naquele nó específico.</span><span class="sxs-lookup"><span data-stu-id="3f673-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="3f673-176">*httpGatewayEndpointPort* Olá porta usados pelo Olá Service Fabric Explorer tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="3f673-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="3f673-177">*ephemeralPorts* substituir Olá [portas dinâmicas usadas pelo Olá OS](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="3f673-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="3f673-178">Service Fabric usará uma parte dessas portas do aplicativo e Olá restantes estarão disponíveis para Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3f673-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="3f673-179">Ele também mapeará esse intervalo toohello intervalo existente presente no hello sistema operacional, então para todas as finalidades, você pode usar intervalos de saudação fornecidos nos arquivos de JSON de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="3f673-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="3f673-180">Você precisa toomake-se de que a diferença Olá entre o início Olá Olá portas e end pelo menos 255.</span><span class="sxs-lookup"><span data-stu-id="3f673-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="3f673-181">Você pode executar em conflitos se essa diferença é muito baixa, pois esse intervalo é compartilhado com o sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f673-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="3f673-182">Consulte o intervalo de portas dinâmicas de saudação configurado executando `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="3f673-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="3f673-183">*applicationPorts* Olá portas que serão usados por aplicativos do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="3f673-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="3f673-184">intervalo de portas de aplicativo Hello deve ser um requisito de ponto de extremidade de saudação toocover grande o suficiente de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3f673-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="3f673-185">Esse intervalo deve ser exclusivo no intervalo de porta dinâmica Olá na máquina hello, ou seja, a saudação de *ephemeralPorts* intervalo conforme definido na configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f673-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="3f673-186">Malha do serviço será usá-los sempre que novas portas são necessárias, bem como o cuidam de abrir o firewall Olá para essas portas.</span><span class="sxs-lookup"><span data-stu-id="3f673-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="3f673-187">*reverseProxyEndpointPort* é um ponto de extremidade de proxy reverso opcional.</span><span class="sxs-lookup"><span data-stu-id="3f673-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="3f673-188">Consulte [Reverter Proxy do Service Fabric](service-fabric-reverseproxy.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="3f673-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="3f673-189">Configurações de log</span><span class="sxs-lookup"><span data-stu-id="3f673-189">Log Settings</span></span>
<span data-ttu-id="3f673-190">Olá **fabricSettings** seção permite que você tooset Olá raiz diretórios Olá Service Fabric dados e logs.</span><span class="sxs-lookup"><span data-stu-id="3f673-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="3f673-191">Você pode personalizar esses somente durante a criação de cluster inicial de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f673-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="3f673-192">Veja abaixo um exemplo de trecho de código desta seção.</span><span class="sxs-lookup"><span data-stu-id="3f673-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="3f673-193">É recomendável usando uma unidade não-OS como Olá FabricDataRoot e FabricLogRoot, pois ele oferece mais confiabilidade contra falhas do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3f673-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="3f673-194">Observe que se você personalizar somente raiz de dados hello, em seguida, raiz de log Olá será colocado um nível abaixo da raiz de dados hello.</span><span class="sxs-lookup"><span data-stu-id="3f673-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="3f673-195">Configurações de Reliable Service com estado</span><span class="sxs-lookup"><span data-stu-id="3f673-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="3f673-196">Olá **KtlLogger** seção permite que você tooset Olá configurações globais para serviços confiáveis.</span><span class="sxs-lookup"><span data-stu-id="3f673-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="3f673-197">Para obter mais detalhes sobre essas configurações, leia [Configurar o Reliable Services com estado](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="3f673-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="3f673-198">exemplo Hello abaixo mostra como toochange Olá Olá compartilhado log de transações que obtém criados tooback todas as coleções confiáveis para serviços com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="3f673-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="3f673-199">Recursos de complemento</span><span class="sxs-lookup"><span data-stu-id="3f673-199">Add-on features</span></span>
<span data-ttu-id="3f673-200">recursos de complemento tooconfigure, Olá apiVersion deve ser configurado como ' 04-2017' ou superior e addonFeatures precisa toobe configurado:</span><span class="sxs-lookup"><span data-stu-id="3f673-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="3f673-201">Suporte a contêiner</span><span class="sxs-lookup"><span data-stu-id="3f673-201">Container support</span></span>
<span data-ttu-id="3f673-202">tooenable suporte de contêiner para o contêiner do windows server e o contêiner do hyper-v para clusters autônomos, recurso de complemento 'DnsService' hello precisa toobe habilitado.</span><span class="sxs-lookup"><span data-stu-id="3f673-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3f673-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f673-203">Next steps</span></span>
<span data-ttu-id="3f673-204">Uma vez que um arquivo Clusterconfig completo configurado de acordo com a configuração de cluster autônomo, você pode implantar o cluster usando o seguinte artigo Olá [criar um cluster do Service Fabric autônomo](service-fabric-cluster-creation-for-windows-server.md) e prossiga muito[visualizar seu cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3f673-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

