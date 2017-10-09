---
title: "aaaSet um cluster do Azure Service Fabric autônomo | Microsoft Docs"
description: "Criar um cluster de autônomo de desenvolvimento com três nós em execução no hello mesmo computador. Depois de concluir esta instalação, você será toocreate pronto um cluster com vários computador."
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
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="38f9c-104">Criar seu primeiro cluster autônomo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="38f9c-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="38f9c-105">Você pode criar um cluster do Service Fabric independentes em quaisquer máquinas virtuais ou computadores que executam o Windows Server 2012 R2 ou Windows Server 2016, local ou na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="38f9c-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in hello cloud.</span></span> <span data-ttu-id="38f9c-106">Este guia de início rápido ajuda toocreate um cluster de desenvolvimento autônomo em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="38f9c-106">This quickstart helps you toocreate a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="38f9c-107">Quando terminar, você terá um cluster de três nós em execução em um único computador no qual poderá implantar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="38f9c-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="38f9c-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="38f9c-108">Before you begin</span></span>
<span data-ttu-id="38f9c-109">Malha do serviço fornece uma configuração de pacote toocreate Service Fabric autônomo clusters.</span><span class="sxs-lookup"><span data-stu-id="38f9c-109">Service Fabric provides a setup package toocreate Service Fabric standalone clusters.</span></span>  <span data-ttu-id="38f9c-110">[Baixar o pacote de instalação Olá](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="38f9c-110">[Download hello setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="38f9c-111">Descompacte Olá pacote tooa pasta de instalação no computador de saudação ou máquina virtual em que você estiver configurando o cluster de desenvolvimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="38f9c-111">Unzip hello setup package tooa folder on hello computer or virtual machine where you are setting up hello development cluster.</span></span>  <span data-ttu-id="38f9c-112">conteúdo Olá Olá do pacote de instalação é descrito em detalhes [aqui](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="38f9c-112">hello contents of hello setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="38f9c-113">administrador de cluster Olá implantar e configurar o cluster Olá deve ter privilégios de administrador no computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="38f9c-113">hello cluster administrator deploying and configuring hello cluster must have administrator privileges on hello computer.</span></span> <span data-ttu-id="38f9c-114">Você não pode instalar o Service Fabric em um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="38f9c-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-hello-environment"></a><span data-ttu-id="38f9c-115">Validar o ambiente de saudação</span><span class="sxs-lookup"><span data-stu-id="38f9c-115">Validate hello environment</span></span>
<span data-ttu-id="38f9c-116">Olá *TestConfiguration.ps1* script no pacote autônomo de saudação é usado como um toovalidate de analisador de práticas recomendada, se um cluster pode ser implantado em um ambiente específico.</span><span class="sxs-lookup"><span data-stu-id="38f9c-116">hello *TestConfiguration.ps1* script in hello standalone package is used as a best practices analyzer toovalidate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="38f9c-117">[Preparação de implantação](service-fabric-cluster-standalone-deployment-preparation.md) listas Olá pré-requisitos e requisitos do ambiente.</span><span class="sxs-lookup"><span data-stu-id="38f9c-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists hello pre-requisites and environment requirements.</span></span> <span data-ttu-id="38f9c-118">Execute Olá script tooverify se você pode criar o cluster de desenvolvimento hello:</span><span class="sxs-lookup"><span data-stu-id="38f9c-118">Run hello script tooverify if you can create hello development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a><span data-ttu-id="38f9c-119">Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="38f9c-119">Create hello cluster</span></span>
<span data-ttu-id="38f9c-120">Vários arquivos de configuração de cluster de exemplo são instalados com o pacote de instalação hello.</span><span class="sxs-lookup"><span data-stu-id="38f9c-120">Several sample cluster configuration files are installed with hello setup package.</span></span> <span data-ttu-id="38f9c-121">*ClusterConfig.Unsecure.DevCluster.json* é a configuração mais simples de cluster Olá: um cluster não seguro, três nós em execução em um único computador.</span><span class="sxs-lookup"><span data-stu-id="38f9c-121">*ClusterConfig.Unsecure.DevCluster.json* is hello simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="38f9c-122">Outros arquivos de configuração descrevem clusters únicos ou vários computadores protegidos com certificados x. 509 ou com a segurança do Windows.</span><span class="sxs-lookup"><span data-stu-id="38f9c-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="38f9c-123">Desnecessários toomodify qualquer uma das definições de configuração saudação padrão para este tutorial, mas examine o arquivo de configuração de saudação e se familiarizar com as configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="38f9c-123">You don't need toomodify any of hello default config settings for this tutorial, but look through hello config file and get familiar with hello settings.</span></span>  <span data-ttu-id="38f9c-124">Olá **nós** seção descreve três nós de cluster Olá Olá: nome, endereço IP, [tipo de nó, o domínio de falha e o domínio de atualização](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="38f9c-124">hello **nodes** section describes hello three nodes in hello cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="38f9c-125">Olá **propriedades** seção define Olá [segurança, nível de confiabilidade, coleta de diagnósticos e tipos de nós](service-fabric-cluster-manifest.md#cluster-properties) para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="38f9c-125">hello **properties** section defines hello [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for hello cluster.</span></span>

<span data-ttu-id="38f9c-126">Esse cluster não é seguro.</span><span class="sxs-lookup"><span data-stu-id="38f9c-126">This cluster is unsecure.</span></span>  <span data-ttu-id="38f9c-127">Qualquer pessoa pode conectar-se anonimamente e realizar operações de gerenciamento, portanto, os clusters de produção sempre devem ser protegidos usando os certificados x.509 ou a segurança do Windows.</span><span class="sxs-lookup"><span data-stu-id="38f9c-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="38f9c-128">Segurança somente é configurada no momento da criação de cluster e não é possível tooenable segurança depois Olá cluster é criado.</span><span class="sxs-lookup"><span data-stu-id="38f9c-128">Security is only configured at cluster creation time and it is not possible tooenable security after hello cluster is created.</span></span>  <span data-ttu-id="38f9c-129">Leitura [proteger um cluster](service-fabric-cluster-security.md) toolearn mais sobre a segurança de cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="38f9c-129">Read [Secure a cluster](service-fabric-cluster-security.md) toolearn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="38f9c-130">cluster de desenvolvimento de três nós Olá toocreate, execute Olá *CreateServiceFabricCluster.ps1* script a partir de uma sessão do PowerShell de administrador:</span><span class="sxs-lookup"><span data-stu-id="38f9c-130">toocreate hello three-node development cluster, run hello *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="38f9c-131">pacote de tempo de execução do Service Fabric Olá automaticamente é baixado e instalado no momento da criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="38f9c-131">hello Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="38f9c-132">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="38f9c-132">Connect toohello cluster</span></span>
<span data-ttu-id="38f9c-133">O cluster de desenvolvimento de três nós agora está em execução.</span><span class="sxs-lookup"><span data-stu-id="38f9c-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="38f9c-134">Olá módulo ServiceFabric do PowerShell é instalado com o tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="38f9c-134">hello ServiceFabric PowerShell module is installed with hello runtime.</span></span>  <span data-ttu-id="38f9c-135">Você pode verificar esse cluster hello está em execução de saudação mesmo computador ou em um computador remoto com o tempo de execução do hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="38f9c-135">You can verify that hello cluster is running from hello same computer or from a remote computer with hello Service Fabric runtime.</span></span>  <span data-ttu-id="38f9c-136">Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet estabelece um cluster de toohello de conexão.</span><span class="sxs-lookup"><span data-stu-id="38f9c-136">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="38f9c-137">Consulte [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para obter outros exemplos de cluster de tooa conexão.</span><span class="sxs-lookup"><span data-stu-id="38f9c-137">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="38f9c-138">Depois de cluster toohello conexão, use Olá [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet uma lista de nós no hello cluster e informações de status para cada nó.</span><span class="sxs-lookup"><span data-stu-id="38f9c-138">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="38f9c-139">**HealthState** deve ser *OK* para cada nó.</span><span class="sxs-lookup"><span data-stu-id="38f9c-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="38f9c-140">Visualizar cluster hello usando o Gerenciador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="38f9c-140">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="38f9c-141">O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma boa ferramenta para visualizar o cluster e gerenciar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="38f9c-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="38f9c-142">Gerenciador do Service Fabric é um serviço que é executado no cluster hello, que você acessa usando um navegador, navegando muito[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="38f9c-142">Service Fabric Explorer is a service that runs in hello cluster, which you access using a browser by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="38f9c-143">painel do cluster Olá fornece uma visão geral do cluster, incluindo um resumo do aplicativo e a integridade do nó.</span><span class="sxs-lookup"><span data-stu-id="38f9c-143">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="38f9c-144">exibição do nó de saudação mostra o layout físico de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="38f9c-144">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="38f9c-145">Para um nó específico, você pode inspecionar quais aplicativos têm código implantado naquele nó.</span><span class="sxs-lookup"><span data-stu-id="38f9c-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a><span data-ttu-id="38f9c-147">Remover cluster Olá</span><span class="sxs-lookup"><span data-stu-id="38f9c-147">Remove hello cluster</span></span>
<span data-ttu-id="38f9c-148">tooremove um cluster, execute Olá *RemoveServiceFabricCluster.ps1* script do PowerShell na pasta de pacote de saudação e passe o arquivo de configuração do hello caminho toohello JSON.</span><span class="sxs-lookup"><span data-stu-id="38f9c-148">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="38f9c-149">Opcionalmente, você pode especificar um local para o log de saudação de exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="38f9c-149">You can optionally specify a location for hello log of hello deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="38f9c-150">Olá tooremove Service Fabric tempo de execução do computador de hello, execute o script do PowerShell a seguir saudação da pasta do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="38f9c-150">tooremove hello Service Fabric runtime from hello computer, run hello following PowerShell script from hello package folder.</span></span>

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="38f9c-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38f9c-151">Next steps</span></span>
<span data-ttu-id="38f9c-152">Agora que você configurou um cluster de desenvolvimento autônomo, tente Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="38f9c-152">Now that you have set up a development standalone cluster, try hello following articles:</span></span>
* <span data-ttu-id="38f9c-153">[Configurar um cluster de vários computadores autônomos](service-fabric-cluster-creation-for-windows-server.md) e habilitar a segurança.</span><span class="sxs-lookup"><span data-stu-id="38f9c-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="38f9c-154">Implantar aplicativos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="38f9c-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
