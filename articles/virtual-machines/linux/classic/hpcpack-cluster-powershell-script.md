---
title: aaaPowerShell script toodeploy cluster HPC do Linux | Microsoft Docs
description: "Executar um toodeploy de script do PowerShell um cluster Linux HPC Pack 2012 R2 em máquinas virtuais do Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="90d74-103">Criar um cluster de computação de alto desempenho (HPC) do Linux com script de implantação de IaaS do HPC Pack Olá</span><span class="sxs-lookup"><span data-stu-id="90d74-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="90d74-104">Execute Olá HPC Pack IaaS implantação PowerShell script toodeploy um cluster de HPC Pack 2012 R2 completo para cargas de trabalho do Linux em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="90d74-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="90d74-105">Olá cluster consiste em um nó principal do Active Directory associado que executam o Windows Server e Microsoft HPC Pack e nós de computação que executam uma saudação distribuições do Linux com suporte pelo pacote de HPC.</span><span class="sxs-lookup"><span data-stu-id="90d74-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="90d74-106">Se você quiser toodeploy um cluster de HPC Pack em cargas de trabalho do Azure para Windows, consulte [criar um cluster do Windows HPC com hello script de implantação IaaS do HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="90d74-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="90d74-107">Você também pode usar um modelo de Gerenciador de recursos do Azure toodeploy um cluster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="90d74-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="90d74-108">Para obter um exemplo, consulte [Criar um cluster HPC com nós de computação Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="90d74-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="90d74-109">Olá script do PowerShell descrito neste artigo cria um cluster do Microsoft HPC Pack 2012 R2 no Azure usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="90d74-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="90d74-110">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="90d74-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="90d74-111">Além disso, o script hello descrito neste artigo não dá suporte a HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="90d74-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="90d74-112">Exemplo de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="90d74-112">Example configuration file</span></span>
<span data-ttu-id="90d74-113">Olá seguinte arquivo de configuração cria um controlador de domínio e floresta de domínio e implanta um cluster de HPC Pack que tem um nó principal com bancos de dados locais e 10 nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="90d74-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="90d74-114">Todos os serviços de nuvem Olá criados diretamente no local do hello Ásia Oriental.</span><span class="sxs-lookup"><span data-stu-id="90d74-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="90d74-115">Olá Linux nós de computação são criados em dois serviços de nuvem e duas contas de armazenamento (ou seja, *MyLnxCN-0001* para *MyLnxCN-0005* na *MyLnxCNService01* e *mylnxstorage01*, e *MyLnxCN-0006* para *MyLnxCN 0010* na *MyLnxCNService02* e *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="90d74-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="90d74-116">nós de computação Olá são criados de uma imagem do Linux OpenLogic CentOS versão 7.0.</span><span class="sxs-lookup"><span data-stu-id="90d74-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="90d74-117">Substitua seus próprios valores para o nome da assinatura e nomes de conta e o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="90d74-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="90d74-118">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="90d74-118">Troubleshooting</span></span>
* <span data-ttu-id="90d74-119">**Erro "VNet não existe"**.</span><span class="sxs-lookup"><span data-stu-id="90d74-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="90d74-120">Se você executar toodeploy de script de implantação de IaaS do HPC Pack Olá vários clusters no Azure simultaneamente em uma assinatura, uma ou mais implantações podem falhar com o erro hello "VNet *VNet\_nome* não existe".</span><span class="sxs-lookup"><span data-stu-id="90d74-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="90d74-121">Se esse erro ocorrer, execute script Olá Olá Falha na implantação.</span><span class="sxs-lookup"><span data-stu-id="90d74-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="90d74-122">**Problema ao acessar Olá Internet da rede virtual do Azure de saudação**.</span><span class="sxs-lookup"><span data-stu-id="90d74-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="90d74-123">Se você criar um cluster de HPC Pack com um novo controlador de domínio usando o script de implantação de hello, ou você promova manualmente um controlador de toodomain VM do nó principal, você pode enfrentar problemas ao conectar Olá VMs em Olá toohello de rede virtual do Azure à Internet.</span><span class="sxs-lookup"><span data-stu-id="90d74-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="90d74-124">Isso pode ocorrer se um servidor DNS encaminhador for configurado automaticamente no controlador de domínio Olá, e esse servidor DNS encaminhador não resolve corretamente.</span><span class="sxs-lookup"><span data-stu-id="90d74-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="90d74-125">toowork alternativa para esse problema, faça logon no controlador de domínio toohello e qualquer definição de configuração do encaminhador de Olá remover ou configurar um servidor DNS encaminhador válido.</span><span class="sxs-lookup"><span data-stu-id="90d74-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="90d74-126">toodo isso, clique no Gerenciador do servidor **ferramentas** > **DNS** tooopen Gerenciador DNS e, em seguida, clique duas vezes em **encaminhadores**.</span><span class="sxs-lookup"><span data-stu-id="90d74-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90d74-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90d74-127">Next steps</span></span>
* <span data-ttu-id="90d74-128">Consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para obter informações sobre distribuições do Linux com suporte, movimentação de dados e envio de cluster de HPC Pack tooan trabalhos com Linux nós de computação.</span><span class="sxs-lookup"><span data-stu-id="90d74-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="90d74-129">Para tutoriais que usam Olá script toocreate um cluster em executar uma carga de trabalho do HPC Linux, consulte:</span><span class="sxs-lookup"><span data-stu-id="90d74-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="90d74-130">Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="90d74-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="90d74-131">Executar o OpenFOAM com o Pacote HPC da Microsoft em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="90d74-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="90d74-132">Executar o STAR-CCM+ com o Pacote HPC da Microsoft em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="90d74-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

