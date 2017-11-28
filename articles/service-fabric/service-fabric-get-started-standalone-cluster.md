---
title: "Configurar um cluster autônomo do Azure Service Fabric | Microsoft Docs"
description: "Crie um cluster de desenvolvimento autônomo com três nós em execução no mesmo computador. Depois de concluir a instalação, você estará pronto para criar um cluster com várias máquinas."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: 5c8f4c784eed7b64810a3dd1c36c043d22a66936
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="41de7-104">Criar seu primeiro cluster autônomo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="41de7-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="41de7-105">Você pode criar um cluster autônomo do Service Fabric em máquinas virtuais ou computadores que executam o Windows Server 2012 R2 ou Windows Server 2016, localmente ou na nuvem.</span><span class="sxs-lookup"><span data-stu-id="41de7-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in the cloud.</span></span> <span data-ttu-id="41de7-106">Este guia de início rápido ajuda a criar um cluster autônomo de desenvolvimento em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="41de7-106">This quickstart helps you to create a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="41de7-107">Quando terminar, você terá um cluster de três nós em execução em um único computador no qual poderá implantar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="41de7-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="41de7-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="41de7-108">Before you begin</span></span>
<span data-ttu-id="41de7-109">O Service Fabric fornece um pacote de instalação para criar clusters autônomos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="41de7-109">Service Fabric provides a setup package to create Service Fabric standalone clusters.</span></span>  <span data-ttu-id="41de7-110">[Baixar o pacote de instalação](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="41de7-110">[Download the setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="41de7-111">Descompacte o pacote de instalação em uma pasta no computador ou máquina virtual na qual você está configurando o cluster de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="41de7-111">Unzip the setup package to a folder on the computer or virtual machine where you are setting up the development cluster.</span></span>  <span data-ttu-id="41de7-112">O conteúdo do pacote de instalação é descrito em detalhes [aqui](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="41de7-112">The contents of the setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="41de7-113">O administrador do cluster que implanta e configura o cluster deve ter privilégios de administrador no computador.</span><span class="sxs-lookup"><span data-stu-id="41de7-113">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span></span> <span data-ttu-id="41de7-114">Você não pode instalar o Service Fabric em um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="41de7-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-the-environment"></a><span data-ttu-id="41de7-115">Validar o ambiente</span><span class="sxs-lookup"><span data-stu-id="41de7-115">Validate the environment</span></span>
<span data-ttu-id="41de7-116">O script *TestConfiguration.ps1* no pacote autônomo é usado como um analisador de práticas recomendadas para validar se um cluster pode ser implantado em um ambiente específico.</span><span class="sxs-lookup"><span data-stu-id="41de7-116">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="41de7-117">[A preparação para implantação](service-fabric-cluster-standalone-deployment-preparation.md) lista os pré-requisitos e requisitos do ambiente.</span><span class="sxs-lookup"><span data-stu-id="41de7-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span></span> <span data-ttu-id="41de7-118">Execute o script para verificar se você pode criar o cluster de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="41de7-118">Run the script to verify if you can create the development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-the-cluster"></a><span data-ttu-id="41de7-119">Criar o cluster</span><span class="sxs-lookup"><span data-stu-id="41de7-119">Create the cluster</span></span>
<span data-ttu-id="41de7-120">Vários arquivos de configuração de cluster de exemplo são instalados com o pacote de instalação.</span><span class="sxs-lookup"><span data-stu-id="41de7-120">Several sample cluster configuration files are installed with the setup package.</span></span> <span data-ttu-id="41de7-121">*ClusterConfig.Unsecure.DevCluster.json* é a configuração de cluster mais simples: um cluster não seguro de três nós em execução em um único computador.</span><span class="sxs-lookup"><span data-stu-id="41de7-121">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="41de7-122">Outros arquivos de configuração descrevem clusters únicos ou vários computadores protegidos com certificados x. 509 ou com a segurança do Windows.</span><span class="sxs-lookup"><span data-stu-id="41de7-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="41de7-123">Você não precisa modificar nenhuma definição de configuração padrão para este tutorial, mas examine o arquivo config e familiarizar-se com as configurações.</span><span class="sxs-lookup"><span data-stu-id="41de7-123">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span></span>  <span data-ttu-id="41de7-124">A seção **Nós** descreve os três nós no cluster: nome, endereço IP, [tipo de nó, domínio de falha e domínio de atualização](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="41de7-124">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="41de7-125">A seção **Propriedades** define a [segurança, nível de confiabilidade, coleta de diagnóstico e tipos de nós](service-fabric-cluster-manifest.md#cluster-properties) para o cluster.</span><span class="sxs-lookup"><span data-stu-id="41de7-125">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span></span>

<span data-ttu-id="41de7-126">Esse cluster não é seguro.</span><span class="sxs-lookup"><span data-stu-id="41de7-126">This cluster is unsecure.</span></span>  <span data-ttu-id="41de7-127">Qualquer pessoa pode conectar-se anonimamente e realizar operações de gerenciamento, portanto, os clusters de produção sempre devem ser protegidos usando os certificados x.509 ou a segurança do Windows.</span><span class="sxs-lookup"><span data-stu-id="41de7-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="41de7-128">A segurança só é configurada no momento de criação do cluster e não é possível habilitar a segurança após a criação dele.</span><span class="sxs-lookup"><span data-stu-id="41de7-128">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span></span>  <span data-ttu-id="41de7-129">Leia [Proteger um cluster](service-fabric-cluster-security.md) para saber mais sobre a segurança do cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="41de7-129">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="41de7-130">Para criar o cluster de desenvolvimento de três nós, execute o script *CreateServiceFabricCluster.ps1* em uma sessão de administrador do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="41de7-130">To create the three-node development cluster, run the *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="41de7-131">O pacote de tempo de execução do Service Fabric é baixado e instalado automaticamente no momento da criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="41de7-131">The Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="41de7-132">Conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="41de7-132">Connect to the cluster</span></span>
<span data-ttu-id="41de7-133">O cluster de desenvolvimento de três nós agora está em execução.</span><span class="sxs-lookup"><span data-stu-id="41de7-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="41de7-134">O módulo ServiceFabric do PowerShell é instalado no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="41de7-134">The ServiceFabric PowerShell module is installed with the runtime.</span></span>  <span data-ttu-id="41de7-135">Você pode verificar se o cluster está em execução no mesmo computador ou em um computador remoto com o tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="41de7-135">You can verify that the cluster is running from the same computer or from a remote computer with the Service Fabric runtime.</span></span>  <span data-ttu-id="41de7-136">O cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) estabelece uma conexão com o cluster.</span><span class="sxs-lookup"><span data-stu-id="41de7-136">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="41de7-137">Confira [Conectar-se a um cluster seguro](service-fabric-connect-to-secure-cluster.md) para obter outros exemplos de como se conectar a um cluster.</span><span class="sxs-lookup"><span data-stu-id="41de7-137">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="41de7-138">Depois de se conectar ao cluster, use o script [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) para exibir uma lista de nós de cluster e informações de status para cada nó.</span><span class="sxs-lookup"><span data-stu-id="41de7-138">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="41de7-139">**HealthState** deve ser *OK* para cada nó.</span><span class="sxs-lookup"><span data-stu-id="41de7-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="41de7-140">Visualizar o cluster usando o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="41de7-140">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="41de7-141">O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma boa ferramenta para visualizar o cluster e gerenciar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="41de7-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="41de7-142">O Service Fabric Explorer é um serviço que é executado no cluster, que você acessa usando um navegador, navegando até [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="41de7-142">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="41de7-143">O painel do cluster fornece uma visão geral do cluster, incluindo um resumo do aplicativo e a integridade do nó.</span><span class="sxs-lookup"><span data-stu-id="41de7-143">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="41de7-144">A exibição de nós mostra o layout físico do cluster.</span><span class="sxs-lookup"><span data-stu-id="41de7-144">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="41de7-145">Para um nó específico, você pode inspecionar quais aplicativos têm código implantado naquele nó.</span><span class="sxs-lookup"><span data-stu-id="41de7-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-the-cluster"></a><span data-ttu-id="41de7-147">Remover o cluster</span><span class="sxs-lookup"><span data-stu-id="41de7-147">Remove the cluster</span></span>
<span data-ttu-id="41de7-148">Para remover um cluster, execute o script do PowerShell *RemoveServiceFabricCluster.ps1* da pasta do pacote e transmita o caminho para o arquivo de configuração JSON.</span><span class="sxs-lookup"><span data-stu-id="41de7-148">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="41de7-149">Como alternativa, você pode especificar um local para o log de exclusão.</span><span class="sxs-lookup"><span data-stu-id="41de7-149">You can optionally specify a location for the log of the deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in the configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="41de7-150">Para remover o tempo de execução do Service Fabric do computador, execute o script do PowerShell a seguir da pasta do pacote.</span><span class="sxs-lookup"><span data-stu-id="41de7-150">To remove the Service Fabric runtime from the computer, run the following PowerShell script from the package folder.</span></span>

```powershell
# Removes Service Fabric from the current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="41de7-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41de7-151">Next steps</span></span>
<span data-ttu-id="41de7-152">Agora que você configurou um cluster de desenvolvimento autônomo, experimente os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="41de7-152">Now that you have set up a development standalone cluster, try the following articles:</span></span>
* <span data-ttu-id="41de7-153">[Configurar um cluster de vários computadores autônomos](service-fabric-cluster-creation-for-windows-server.md) e habilitar a segurança.</span><span class="sxs-lookup"><span data-stu-id="41de7-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="41de7-154">Implantar aplicativos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="41de7-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
