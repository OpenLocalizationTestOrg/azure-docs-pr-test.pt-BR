---
title: cluster do Windows HPC aaaPowerShell script toodeploy | Microsoft Docs
description: "Executar um toodeploy de script do PowerShell um cluster do Windows HPC Pack 2012 R2 em máquinas virtuais do Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="e8410-103">Criar um cluster de computação de alto desempenho (HPC) do Windows com o script de implantação de IaaS do HPC Pack Olá</span><span class="sxs-lookup"><span data-stu-id="e8410-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="e8410-104">Execute Olá HPC Pack IaaS implantação PowerShell script toodeploy um cluster de HPC Pack 2012 R2 completo para cargas de trabalho do Windows em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8410-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="e8410-105">Olá cluster consiste em um nó principal do Active Directory associado que executam o Windows Server e Microsoft HPC Pack e janelas adicionais de computação recursos que você especificar.</span><span class="sxs-lookup"><span data-stu-id="e8410-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="e8410-106">Se você quiser toodeploy um cluster de HPC Pack no Azure para cargas de trabalho do Linux, consulte [criar um cluster de HPC Linux com hello script de implantação IaaS do HPC Pack](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="e8410-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="e8410-107">Você também pode usar um modelo de Gerenciador de recursos do Azure toodeploy um cluster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="e8410-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="e8410-108">Para obter exemplos, confira [Criar um cluster HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) e [Criar um cluster HPC com uma imagem do nó de computação personalizada](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span><span class="sxs-lookup"><span data-stu-id="e8410-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e8410-109">Olá script do PowerShell descrito neste artigo cria um cluster do Microsoft HPC Pack 2012 R2 no Azure usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="e8410-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="e8410-110">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8410-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="e8410-111">Além disso, o script hello descrito neste artigo não dá suporte a HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="e8410-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="e8410-112">Exemplo de arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="e8410-112">Example configuration files</span></span>
<span data-ttu-id="e8410-113">Olá exemplos a seguir, substitua seus próprios valores para a Id da assinatura ou nome e nomes de conta e o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8410-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="e8410-114">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="e8410-114">Example 1</span></span>
<span data-ttu-id="e8410-115">Olá seguinte arquivo de configuração implanta um cluster de HPC Pack que tem cinco nós de computação executando o sistema de operacional do Windows Server 2012 R2 hello e um nó principal com bancos de dados locais.</span><span class="sxs-lookup"><span data-stu-id="e8410-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="e8410-116">Todos os serviços de nuvem Olá são criados diretamente no hello local Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="e8410-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="e8410-117">nó principal Olá atua como controlador de domínio da floresta de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="e8410-117">hello head node acts as domain controller of hello domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="e8410-118">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="e8410-118">Example 2</span></span>
<span data-ttu-id="e8410-119">Olá, arquivo de configuração a seguir implanta um cluster de HPC Pack em uma floresta de domínio existente.</span><span class="sxs-lookup"><span data-stu-id="e8410-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="e8410-120">cluster Olá tem 1 nó principal com bancos de dados locais e 12 nós com hello extensão BGInfo VM aplicada de computação.</span><span class="sxs-lookup"><span data-stu-id="e8410-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="e8410-121">A instalação automática de atualizações do Windows está desabilitada para Olá todas as VMs na floresta de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="e8410-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="e8410-122">Todos os serviços de nuvem Olá são criados diretamente no local Ásia Oriental.</span><span class="sxs-lookup"><span data-stu-id="e8410-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="e8410-123">nós de computação Olá são criados em três serviços de nuvem e três contas de armazenamento: *MyHPCCN-0001* muito*MyHPCCN-0005* na *MyHPCCNService01* e  *mycnstorage01*; *MyHPCCN-0006* muito*MyHPCCN0010* na *MyHPCCNService02* e *mycnstorage02*; e  *MyHPCCN-0011* muito*MyHPCCN-0012* na *MyHPCCNService03* e *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="e8410-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="e8410-124">nós de computação Olá são criados de uma imagem privada existente capturada de um nó de computação.</span><span class="sxs-lookup"><span data-stu-id="e8410-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="e8410-125">Olá automaticamente aumentar ou reduzir serviço está habilitado com padrão ampliar ou reduzir os intervalos.</span><span class="sxs-lookup"><span data-stu-id="e8410-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="e8410-126">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="e8410-126">Example 3</span></span>
<span data-ttu-id="e8410-127">Olá, arquivo de configuração a seguir implanta um cluster de HPC Pack em uma floresta de domínio existente.</span><span class="sxs-lookup"><span data-stu-id="e8410-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="e8410-128">cluster Olá contém um nó de cabeçalho, um servidor de banco de dados com um disco de dados de 500 GB, dois nós do agente executando o sistema de operacional do Windows Server 2012 R2 hello e cinco nós de computação executando o sistema de operacional do Windows Server 2012 R2 hello.</span><span class="sxs-lookup"><span data-stu-id="e8410-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="e8410-129">Olá MyHPCCNService é criado no grupo de afinidade de saudação do serviço de nuvem *MyIBAffinityGroup*, e hello outros serviços em nuvem são criados no grupo de afinidade Olá *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="e8410-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="e8410-130">Olá API de REST do Agendador de trabalho do HPC e o portal da web do HPC estão habilitados no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="e8410-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="e8410-131">Exemplo 4</span><span class="sxs-lookup"><span data-stu-id="e8410-131">Example 4</span></span>
<span data-ttu-id="e8410-132">Olá, arquivo de configuração a seguir implanta um cluster de HPC Pack em uma floresta de domínio existente.</span><span class="sxs-lookup"><span data-stu-id="e8410-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="e8410-133">cluster Olá tem dois nó principal com bancos de dados locais, dois modelos de nó do Azure são criados e três nós do tamanho médio Azure são criados para o modelo de nó do Azure *AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="e8410-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="e8410-134">Um arquivo de script é executado no nó principal Olá após a configuração do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="e8410-134">A script file runs on hello head node after hello head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="e8410-135">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e8410-135">Troubleshooting</span></span>
* <span data-ttu-id="e8410-136">**Erro "VNet não existe"** -se você executar Olá script toodeploy vários clusters no Azure simultaneamente em uma assinatura, uma ou mais implantações podem falhar com o erro hello "VNet *VNet\_nome* não existe".</span><span class="sxs-lookup"><span data-stu-id="e8410-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="e8410-137">Se esse erro ocorrer, execute o script de saudação novamente para Olá Falha na implantação.</span><span class="sxs-lookup"><span data-stu-id="e8410-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="e8410-138">**Problema ao acessar Olá Internet da rede virtual do Azure de saudação** - se criar um cluster com um novo controlador de domínio usando o script de implantação hello, ou manualmente promover um controlador de toodomain VM do nó principal, você pode enfrentar problemas Conectando Olá VMs toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="e8410-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="e8410-139">Esse problema pode ocorrer se um servidor DNS encaminhador for configurado automaticamente no controlador de domínio Olá, e esse servidor DNS encaminhador não resolve corretamente.</span><span class="sxs-lookup"><span data-stu-id="e8410-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="e8410-140">toowork alternativa para esse problema, faça logon no controlador de domínio toohello e qualquer definição de configuração do encaminhador de Olá remover ou configurar um servidor DNS encaminhador válido.</span><span class="sxs-lookup"><span data-stu-id="e8410-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="e8410-141">tooconfigure essa configuração, no Gerenciador de servidores clique **ferramentas** >
    **DNS** tooopen Gerenciador DNS e, em seguida, clique duas vezes em **encaminhadores**.</span><span class="sxs-lookup"><span data-stu-id="e8410-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="e8410-142">**Problema ao acessar a rede RDMA de VMs de computação intensa** - se adicionar computadores Windows Server ou nó do agente usando um compatíveis com RDMA de VMs de tamanho, como A8 ou A9, você pode enfrentar problemas de conexão de rede do aplicativo essas VMs toohello RDMA.</span><span class="sxs-lookup"><span data-stu-id="e8410-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="e8410-143">Um motivo que ocorrer esse problema é se Olá extensão HpcVmDrivers não está instalado corretamente quando Olá VMs são adicionadas toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="e8410-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="e8410-144">Por exemplo, a extensão pode estar paralisada na Olá estado de instalação.</span><span class="sxs-lookup"><span data-stu-id="e8410-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="e8410-145">toowork alternativa para esse problema, primeiro verificar Olá estado da extensão Olá Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="e8410-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="e8410-146">Se a extensão de saudação não está instalado corretamente, tente remover nós de saudação do cluster HPC hello e adicione nós Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="e8410-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="e8410-147">Por exemplo, você pode adicionar o nó de computação VMs executando o script Add-hpciaasnode.ps1 de saudação no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="e8410-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8410-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8410-148">Next steps</span></span>
* <span data-ttu-id="e8410-149">Tente executar uma carga de trabalho de teste no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8410-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="e8410-150">Para obter um exemplo, consulte Olá HPC Pack [guia de Introdução](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="e8410-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="e8410-151">Para um tutorial tooscript Olá a implantação de cluster e execute uma carga de trabalho do HPC, consulte [começar com um cluster de HPC Pack em cargas de trabalho do Excel e SOA Azure toorun](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8410-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="e8410-152">Tente toostart de ferramentas do HPC Pack, parar, adicionar e remover nós de computação de um cluster que você criar.</span><span class="sxs-lookup"><span data-stu-id="e8410-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="e8410-153">Consulte [Gerenciar nós de computação em um cluster de Pacote HPC no Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="e8410-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="e8410-154">tooget configurar o cluster de toohello trabalhos toosubmit de um computador local, consulte [cluster trabalhos de HPC de envio de um computador de local tooan HPC Pack no Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8410-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

