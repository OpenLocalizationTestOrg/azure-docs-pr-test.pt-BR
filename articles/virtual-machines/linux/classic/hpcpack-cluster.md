---
title: "VMs de computação do Linux em um cluster de HPC Pack | Microsoft Docs"
description: "Saiba como criar e usar um cluster HPC Pack em cargas de trabalho HPC (computação de alto desempenho) no Azure para Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 809d3944311badf265117d353b65642e044d900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="fff14-103">Introdução a nós de computação Linux em um cluster de HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="fff14-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="fff14-104">Configure um cluster do [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) no Azure que contenha um nó de cabeçalho que executa o Windows Server e vários nós de computação que executam uma distribuição do Linux com suporte.</span><span class="sxs-lookup"><span data-stu-id="fff14-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="fff14-105">Explore as opções para mover dados entre nós Linux e o nó principal do Windows do cluster.</span><span class="sxs-lookup"><span data-stu-id="fff14-105">Explore options to move data among the Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="fff14-106">Saiba como enviar trabalhos do HPC Linux para o cluster.</span><span class="sxs-lookup"><span data-stu-id="fff14-106">Learn how to submit Linux HPC jobs to the cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="fff14-107">Em um alto nível, o diagrama a seguir mostra o cluster HPC Pack que você criará e com que trabalhará.</span><span class="sxs-lookup"><span data-stu-id="fff14-107">At a high level, the following diagram shows the HPC Pack cluster you create and work with.</span></span>

![Cluster HPC Pack com nós Linux][scenario]

<span data-ttu-id="fff14-109">Para obter outras opções para executar cargas de trabalho HPC Linux no Azure, consulte [Recursos técnicos para computação em lote e de alto desempenho](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fff14-109">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="fff14-110">Implantar um cluster de HPC Pack com nós de computação Linux</span><span class="sxs-lookup"><span data-stu-id="fff14-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="fff14-111">Este artigo mostra duas opções para implantar um cluster do HPC Pack no Azure com nós de computação Linux .</span><span class="sxs-lookup"><span data-stu-id="fff14-111">This article shows you two options to deploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="fff14-112">Os dois métodos usam uma imagem do Marketplace do Windows Server com HPC Pack para criar o nó principal.</span><span class="sxs-lookup"><span data-stu-id="fff14-112">Both methods use a Marketplace image of Windows Server with HPC Pack to create the head node.</span></span> 

* <span data-ttu-id="fff14-113">**Modelo do Azure Resource Manager** – Use um modelo do Azure Marketplace ou um modelo de início rápido da comunidade para automatizar a criação do cluster no modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fff14-113">**Azure Resource Manager template** - Use a template from the Azure Marketplace, or a quickstart template from the community, to automate creation of the cluster in the Resource Manager deployment model.</span></span> <span data-ttu-id="fff14-114">Por exemplo, o modelo de [Cluster do HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) no Azure Marketplace cria uma infraestrutura completa de cluster de HPC Pack para cargas de trabalho do HPC no Linux.</span><span class="sxs-lookup"><span data-stu-id="fff14-114">For example, the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="fff14-115">**Script do PowerShell** - [use o script de implantação de IaaS do Microsoft HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) para automatizar uma implantação de cluster completa no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="fff14-115">**PowerShell script** - Use the [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) to automate a complete cluster deployment in the classic deployment model.</span></span> <span data-ttu-id="fff14-116">Esse script do Azure PowerShell usa uma imagem de VM do HPC Pack no Azure Marketplace para implantação rápida e fornece um conjunto abrangente de parâmetros de configuração para implantar nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="fff14-116">This Azure PowerShell script uses an HPC Pack VM image in the Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters to deploy Linux compute nodes.</span></span>

<span data-ttu-id="fff14-117">Para obter mais informações sobre as opções de implantação de cluster do HPC Pack, consulte [Opções para criar e gerenciar um cluster de HPC (computação de alto desempenho ) no Azure com o Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fff14-117">For more information about HPC Pack cluster deployment options in Azure, see [Options to create and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fff14-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fff14-118">Prerequisites</span></span>
* <span data-ttu-id="fff14-119">**Assinatura do Azure** : você pode usar a assinatura no serviço Azure Global ou no Azure China.</span><span class="sxs-lookup"><span data-stu-id="fff14-119">**Azure subscription** - You can use a subscription in either the Azure Global or Azure China service.</span></span> <span data-ttu-id="fff14-120">Se você não tem uma conta, pode criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="fff14-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="fff14-121">**Cota para núcleos** – talvez seja necessário aumentar a cota de núcleos, especialmente se você optar por implantar vários nós de cluster com tamanhos de VM de vários núcleos.</span><span class="sxs-lookup"><span data-stu-id="fff14-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="fff14-122">Para aumentar a cota, abra uma solicitação de atendimento ao cliente online gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="fff14-122">To increase a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="fff14-123">**Distribuições Linux** -atualmente, o HPC Pack dá suporte às distribuições Linux a seguir para nós de computação.</span><span class="sxs-lookup"><span data-stu-id="fff14-123">**Linux distributions** - Currently HPC Pack supports the following Linux distributions for compute nodes.</span></span> <span data-ttu-id="fff14-124">Você pode usar as versões do Marketplace dessas distribuições quando disponíveis ou fornecer as suas próprias.</span><span class="sxs-lookup"><span data-stu-id="fff14-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="fff14-125">**Com base em centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, HPC 6.5, HPC 7.1</span><span class="sxs-lookup"><span data-stu-id="fff14-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="fff14-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="fff14-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="fff14-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 para HPC, SLES 12 para HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="fff14-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="fff14-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="fff14-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="fff14-129">Para usar a rede RDMA do Azure com um dos tamanhos de VM compatíveis com RDMA, especifique uma imagem de HPC com base em CentOS ou de HPC do SUSE Linux Enterprise Server 12 no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fff14-129">To use the Azure RDMA network with one of the RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from the Azure Marketplace.</span></span> <span data-ttu-id="fff14-130">Para obter mais informações, consulte [Tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fff14-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="fff14-131">Pré-requisitos adicionais para implantar o cluster usando o script de implantação de IaaS do HPC Pack:</span><span class="sxs-lookup"><span data-stu-id="fff14-131">Additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="fff14-132">**Computador cliente** – você precisa de um computador cliente com Windows para executar o script de implantação do cluster.</span><span class="sxs-lookup"><span data-stu-id="fff14-132">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="fff14-133">**Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="fff14-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="fff14-134">**Script de implantação de IaaS do HPC Pack** – baixe e descompacte a versão mais recente do script no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="fff14-134">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="fff14-135">Verifique a versão do script executando `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="fff14-135">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="fff14-136">Este artigo se baseia na versão 4.4.1 ou posterior do script.</span><span class="sxs-lookup"><span data-stu-id="fff14-136">This article is based on version 4.4.1 or later of the script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="fff14-137">Opção de implantação 1.</span><span class="sxs-lookup"><span data-stu-id="fff14-137">Deployment option 1.</span></span> <span data-ttu-id="fff14-138">Use um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fff14-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="fff14-139">Vá para o modelo [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) no Azure Marketplace e clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="fff14-139">Go to the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="fff14-140">No portal do Azure, examine as informações e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fff14-140">In the Azure portal, review the information and then click **Create**.</span></span>
   
    ![Criação de portal][portal]
3. <span data-ttu-id="fff14-142">Na folha **Noções básicas** , insira um nome para o cluster, que também será o nome da VM do nó principal.</span><span class="sxs-lookup"><span data-stu-id="fff14-142">On the **Basics** blade, enter a name for the cluster, which also names the head node VM.</span></span> <span data-ttu-id="fff14-143">Você pode escolher um grupo de recursos existente ou criar um novo grupo de recursos para a implantação em um local que está disponível para você.</span><span class="sxs-lookup"><span data-stu-id="fff14-143">You can choose an existing resource group or create a group for the deployment in a location that's available to you.</span></span> <span data-ttu-id="fff14-144">O local afeta a disponibilidade de determinados tamanhos de VM e outros serviços do Azure (consulte [produtos disponíveis por região](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="fff14-144">The location affects the availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="fff14-145">Na folha **Configurações do nó de cabeçalho** , para uma primeira implantação, geralmente você aceitará as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="fff14-145">On the **Head node settings** blade, for a first deployment, you can generally accept the default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="fff14-146">A **URL do script pós-configuração** é uma configuração opcional para especificar um script do Windows PowerShell publicamente disponível que você deseja executar na VM do nó principal depois que ela estiver em execução.</span><span class="sxs-lookup"><span data-stu-id="fff14-146">The **Post-configuration script URL** is an optional setting to specify a publicly available Windows PowerShell script that you want to run on the head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="fff14-147">Na folha **Configurações de nós de computação** , selecione um padrão de nomenclatura para os nós, o número e o tamanho dos nós e a distribuição Linux a implantar.</span><span class="sxs-lookup"><span data-stu-id="fff14-147">On the **Compute node settings** blade, select a naming pattern for the nodes, the number and size of the nodes, and the Linux distribution to deploy.</span></span>
6. <span data-ttu-id="fff14-148">Na folha **Configurações de infraestrutura** , insira nomes para a rede virtual e o domínio do Active Directory, para as credenciais de administrador do domínio e da VM e um padrão de nomenclatura para as contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fff14-148">On the **Infrastructure settings** blade, enter names for the virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for the storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fff14-149">O HPC Pack usa o domínio do Active Directory para autenticar usuários de cluster.</span><span class="sxs-lookup"><span data-stu-id="fff14-149">HPC Pack uses the Active Directory domain to authenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="fff14-150">Depois de executar os testes de validação e examinar os termos de uso, clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="fff14-150">After the validation tests run and you review the terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-the-iaas-deployment-script"></a><span data-ttu-id="fff14-151">Opção de implantação 2.</span><span class="sxs-lookup"><span data-stu-id="fff14-151">Deployment option 2.</span></span> <span data-ttu-id="fff14-152">Usar o script de implantação de IaaS do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="fff14-152">Use the IaaS deployment script</span></span>
<span data-ttu-id="fff14-153">A seguir estão pré-requisitos adicionais para implantar o cluster usando o script de implantação de IaaS do HPC Pack:</span><span class="sxs-lookup"><span data-stu-id="fff14-153">Following are additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="fff14-154">**Computador cliente** – você precisa de um computador cliente com Windows para executar o script de implantação do cluster.</span><span class="sxs-lookup"><span data-stu-id="fff14-154">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="fff14-155">**Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="fff14-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="fff14-156">**Script de implantação de IaaS do HPC Pack** – baixe e descompacte a versão mais recente do script no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="fff14-156">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="fff14-157">Verifique a versão do script executando `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="fff14-157">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="fff14-158">Este artigo se baseia na versão 4.4.1 ou posterior do script.</span><span class="sxs-lookup"><span data-stu-id="fff14-158">This article is based on version 4.4.1 or later of the script.</span></span>

<span data-ttu-id="fff14-159">**Arquivo de configuração XML**</span><span class="sxs-lookup"><span data-stu-id="fff14-159">**XML configuration file**</span></span>

<span data-ttu-id="fff14-160">O script de implantação do HPC Pack de IaaS usa um arquivo de configuração XML como entrada para descrever o cluster do HPC.</span><span class="sxs-lookup"><span data-stu-id="fff14-160">The HPC Pack IaaS deployment script uses an XML configuration file as input to describe the  HPC cluster.</span></span> <span data-ttu-id="fff14-161">O arquivo de configuração de exemplo a seguir especifica um pequeno cluster, que consiste em um nó principal do HPC Pack e em dois nós de computação do Linux CentOS 7.0 de tamanho A7.</span><span class="sxs-lookup"><span data-stu-id="fff14-161">The following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="fff14-162">Modifique o arquivo como necessário para seu ambiente e a configuração de cluster desejada e salve-o com um nome como HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="fff14-162">Modify the file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="fff14-163">Por exemplo, você precisa fornecer seu nome de assinatura e um nome de conta de armazenamento exclusivo e o nome do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="fff14-163">For example, you need to supply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="fff14-164">Além disso, convém escolher uma imagem diferente do Linux com suporte para os nós de computação.</span><span class="sxs-lookup"><span data-stu-id="fff14-164">Additionally, you might want to choose a different supported Linux image for the compute nodes.</span></span> <span data-ttu-id="fff14-165">Para saber mais sobre os elementos no arquivo de configuração, veja o arquivo Manual.rtf na pasta scripts e [Criar um cluster HPC com o script de implantação de IaaS do HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fff14-165">For more information about the elements in the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="fff14-166">**Para executar o script de implantação de IaaS do HPC Pack**</span><span class="sxs-lookup"><span data-stu-id="fff14-166">**To run the HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="fff14-167">Abra o console do Windows PowerShell no computador cliente como administrador.</span><span class="sxs-lookup"><span data-stu-id="fff14-167">Open Windows PowerShell on the client computer as an administrator.</span></span>
2. <span data-ttu-id="fff14-168">Altere o diretório para a pasta onde os scripts estão instalados (E:\IaaSClusterScript neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="fff14-168">Change directory to the folder where the script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="fff14-169">Execute o comando a seguir para implantar o cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="fff14-169">Run the following command to deploy the HPC Pack cluster.</span></span> <span data-ttu-id="fff14-170">Este exemplo supõe que o arquivo de configuração esteja localizado em E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="fff14-170">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="fff14-171">a.</span><span class="sxs-lookup"><span data-stu-id="fff14-171">a.</span></span> <span data-ttu-id="fff14-172">Como a **AdminPassword** não é especificada no comando anterior, você deve inserir a senha para o usuário *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="fff14-172">Because the **AdminPassword** is not specified in the preceding command, you are prompted to enter the password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="fff14-173">b.</span><span class="sxs-lookup"><span data-stu-id="fff14-173">b.</span></span> <span data-ttu-id="fff14-174">Em seguida, o script começa a validar o arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="fff14-174">The script then starts to validate the configuration file.</span></span> <span data-ttu-id="fff14-175">Pode demorar dezenas de segundos a vários minutos dependendo da conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="fff14-175">It can take up to several minutes depending on the network connection.</span></span>
   
    ![Validação][validate]
   
    <span data-ttu-id="fff14-177">c.</span><span class="sxs-lookup"><span data-stu-id="fff14-177">c.</span></span> <span data-ttu-id="fff14-178">Depois de passarem as validações, o script lista os recursos de cluster a serem criados.</span><span class="sxs-lookup"><span data-stu-id="fff14-178">After validations pass, the script lists the cluster resources to create.</span></span> <span data-ttu-id="fff14-179">Digite *y* para continuar.</span><span class="sxs-lookup"><span data-stu-id="fff14-179">Enter *Y* to continue.</span></span>
   
    ![Recursos][resources]
   
    <span data-ttu-id="fff14-181">d.</span><span class="sxs-lookup"><span data-stu-id="fff14-181">d.</span></span> <span data-ttu-id="fff14-182">O script começa a implantar o cluster de HPC Pack e concluirá a configuração sem outras etapas manuais.</span><span class="sxs-lookup"><span data-stu-id="fff14-182">The script starts to deploy the HPC Pack cluster and completes the configuration without further manual steps.</span></span> <span data-ttu-id="fff14-183">O script pode ser executado por vários minutos.</span><span class="sxs-lookup"><span data-stu-id="fff14-183">The script can run for several minutes.</span></span>
   
    ![Implantar][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="fff14-185">Neste exemplo, o script gera um arquivo de log automaticamente, pois o parâmetro **-LogFile** não está especificado.</span><span class="sxs-lookup"><span data-stu-id="fff14-185">In this example, the script generates a log file automatically since the **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="fff14-186">Os logs não são gravados em tempo real, mas são coletados no final da validação e na implantação.</span><span class="sxs-lookup"><span data-stu-id="fff14-186">The logs aren't written in real time, but are collected at the end of the validation and the deployment.</span></span> <span data-ttu-id="fff14-187">Se o processo do PowerShell for interrompido durante a execução do script, alguns logs serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="fff14-187">If the PowerShell process is stopped while the script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-to-the-head-node"></a><span data-ttu-id="fff14-188">Conectar-se ao nó principal</span><span class="sxs-lookup"><span data-stu-id="fff14-188">Connect to the head node</span></span>
<span data-ttu-id="fff14-189">Depois de implantar o cluster do HPC Pack no Azure, [conecte-se por meio da Área de Trabalho Remota](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à VM do nó principal usando o domínio credenciais fornecidas quando você implantou o cluster (por exemplo, *hpc\\clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="fff14-189">After you deploy the HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="fff14-190">Você gerencia o cluster do nó principal.</span><span class="sxs-lookup"><span data-stu-id="fff14-190">You manage the cluster from the head node.</span></span>

<span data-ttu-id="fff14-191">No nó principal, inicie o Gerenciador de Cluster HPC para verificar o status do cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="fff14-191">On the head node, start HPC Cluster Manager to check the status of the HPC Pack cluster.</span></span> <span data-ttu-id="fff14-192">Você pode gerenciar e monitorar os nós de computação Linux da mesma maneira que faz trabalha com os nós de computação do Windows.</span><span class="sxs-lookup"><span data-stu-id="fff14-192">You can manage and monitor Linux compute nodes the same way you work with Windows compute nodes.</span></span> <span data-ttu-id="fff14-193">Por exemplo, você verá os nós Linux listados no**Resource Management** (esses nós são implantados com o modelo **LinuxNode**).</span><span class="sxs-lookup"><span data-stu-id="fff14-193">For example, you see the Linux nodes listed in **Resource Management** (these nodes are deployed with the **LinuxNode** template).</span></span>

![Gerenciamento de nós][management]

<span data-ttu-id="fff14-195">Você também verá os nós Linux na exibição do **Mapa de Calor** .</span><span class="sxs-lookup"><span data-stu-id="fff14-195">You also see the Linux nodes in the **Heat Map** view.</span></span>

![Mapa de Calor][heatmap]

## <a name="how-to-move-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="fff14-197">Como mover dados em um cluster com nós do Linux</span><span class="sxs-lookup"><span data-stu-id="fff14-197">How to move data in a cluster with Linux nodes</span></span>
<span data-ttu-id="fff14-198">Você tem várias opções para mover dados entre nós Linux e o nó principal do Windows do cluster.</span><span class="sxs-lookup"><span data-stu-id="fff14-198">You have several choices to move data among Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="fff14-199">Aqui estão três métodos comuns, descritos mais detalhadamente nas seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="fff14-199">Here are three common methods, described in more detail in the following sections:</span></span>

* <span data-ttu-id="fff14-200">**Arquivo do Azure** – expõe um compartilhamento de arquivos SMB gerenciado para armazenar arquivos de dados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fff14-200">**Azure File** - Exposes a managed SMB file share to store data files in Azure storage.</span></span> <span data-ttu-id="fff14-201">Os nós do Windows e do Linux poderão montar um compartilhamento de Arquivos do Azure como uma unidade ou pasta ao mesmo tempo, mesmo se eles estiverem implantados em diferentes redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="fff14-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at the same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="fff14-202">**Compartilhamento do nó de cabeçalho SMB** – monta uma pasta compartilhada padrão do Windows do nó de cabeçalho em nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="fff14-202">**Head node SMB share** - Mounts a standard Windows shared folder of the head node on Linux nodes.</span></span>
* <span data-ttu-id="fff14-203">**Servidor NFS do nó de cabeçalho** – fornece uma solução de compartilhamento de arquivos para um ambiente misto do Windows e do Linux.</span><span class="sxs-lookup"><span data-stu-id="fff14-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="fff14-204">Armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="fff14-204">Azure File storage</span></span>
<span data-ttu-id="fff14-205">O serviço [Arquivo do Azure](https://azure.microsoft.com/services/storage/files/) expõe os compartilhamentos de arquivos usando o protocolo SMB 2.1 padrão.</span><span class="sxs-lookup"><span data-stu-id="fff14-205">The [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using the standard SMB 2.1 protocol.</span></span> <span data-ttu-id="fff14-206">As VMs e os serviços de nuvem podem compartilhar dados de arquivos entre componentes de aplicativos por meio de compartilhamentos montados, e aplicativos locais podem acessar dados de arquivos em um compartilhamento por meio da API de armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="fff14-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through the File storage API.</span></span> 

<span data-ttu-id="fff14-207">Para obter etapas detalhadas para criar um compartilhamento de Arquivos do Azure e montá-lo no nó principal, veja [Introdução ao armazenamento de Arquivos do Azure no Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="fff14-207">For detailed steps to create an Azure File share and mount it on the head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="fff14-208">Para montar o compartilhamento de Arquivos do Azure em nós do Linux, consulte [Como usar o armazenamento de Arquivos do Azure com Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fff14-208">To mount the Azure File share on the Linux nodes, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="fff14-209">Para configurar as conexões persistentes, confira [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="fff14-209">To set up persisting connections, see [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="fff14-210">No exemplo a seguir, crie um compartilhamento de arquivos do Azure em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fff14-210">In the following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="fff14-211">Para montar o compartilhamento no nó de cabeçalho, abra um Prompt de Comando e insira os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fff14-211">To mount the share on the head node, open a Command Prompt and enter the following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="fff14-212">Neste exemplo, allvhdsje é o nome da conta de armazenamento, storageaccountkey é a chave de conta de armazenamento e o rdma é o nome do compartilhamento de arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fff14-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is the Azure File share name.</span></span> <span data-ttu-id="fff14-213">O compartilhamento de Arquivos do Azure é montado como Z: no nó principal.</span><span class="sxs-lookup"><span data-stu-id="fff14-213">The Azure File share is mounted as Z: on the head node.</span></span>

<span data-ttu-id="fff14-214">Para montar o compartilhamento de Arquivo do Azure em nós do Linux, execute um comando **clusrun** no nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="fff14-214">To mount the Azure File share on Linux nodes, run a **clusrun** command on the head node.</span></span> <span data-ttu-id="fff14-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** é uma ferramenta útil do HPC Pack para executar tarefas administrativas em vários nós.</span><span class="sxs-lookup"><span data-stu-id="fff14-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool to carry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="fff14-216">(Consulte também [Clusrun para nós Linux](#Clusrun-for-Linux-nodes) neste artigo.)</span><span class="sxs-lookup"><span data-stu-id="fff14-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="fff14-217">Abra uma janela do Windows PowerShell e digite os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fff14-217">Open a Windows PowerShell window and enter the following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="fff14-218">O primeiro comando cria uma pasta chamada /rdma em todos os nós do grupo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="fff14-218">The first command creates a folder named /rdma on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="fff14-219">O segundo comando monta a pasta allvhdsjw.file.core.windows.net/rdma de compartilhamento de Arquivos do Azure para a pasta /rdma com dir e bits de modo de arquivo definido como 777.</span><span class="sxs-lookup"><span data-stu-id="fff14-219">The second command mounts the Azure File share allvhdsjw.file.core.windows.net/rdma onto the /rdma folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="fff14-220">No segundo comando, allvhdsje é o nome da sua conta de armazenamento e storageaccountkey é a chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fff14-220">In the second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="fff14-221">O símbolo "\\`" no segundo comando é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fff14-221">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="fff14-222">"\\`," significa que "," (uma vírgula) é uma parte do comando.</span><span class="sxs-lookup"><span data-stu-id="fff14-222">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="fff14-223">Compartilhamento do nó principal</span><span class="sxs-lookup"><span data-stu-id="fff14-223">Head node share</span></span>
<span data-ttu-id="fff14-224">Como alternativa, monte uma pasta compartilhada do nó de cabeçalho em nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="fff14-224">Alternatively, mount a shared folder of the head node on Linux nodes.</span></span> <span data-ttu-id="fff14-225">Um compartilhamento é a maneira mais simples de compartilhar arquivos, mas o nó principal e todos os nós do Linux precisam ser implantados na mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fff14-225">A share provides the simplest way to share files, but the head node and all Linux nodes must be deployed in the same virtual network.</span></span> <span data-ttu-id="fff14-226">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="fff14-226">Here are the steps.</span></span>

1. <span data-ttu-id="fff14-227">Crie uma pasta no nó principal e compartilhe-o com Todos com permissões de Leitura/Gravação.</span><span class="sxs-lookup"><span data-stu-id="fff14-227">Create a folder on the head node and share it to Everyone with Read/Write permissions.</span></span> <span data-ttu-id="fff14-228">Por exemplo, compartilhe D:\OpenFOAM no nó de cabeçalho como \\CentOS7RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="fff14-228">For example, share D:\OpenFOAM on the head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="fff14-229">Nesse caso, o CentOS7RDMA-HN é o nome do host do nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="fff14-229">Here CentOS7RDMA-HN is the hostname of the head node.</span></span>
   
    ![Permissões de compartilhamento de arquivo][fileshareperms]
   
    ![Compartilhamento de arquivos][filesharing]
2. <span data-ttu-id="fff14-232">Abra uma janela do Windows PowerShell e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fff14-232">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="fff14-233">O primeiro comando cria uma pasta chamada /openfoam em todos os nós no grupo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="fff14-233">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="fff14-234">O segundo comando monta a pasta compartilhada //CentOS7RDMA-HN/OpenFOAM para a pasta com dir e bits de modo de arquivo definido como 777.</span><span class="sxs-lookup"><span data-stu-id="fff14-234">The second command mounts the shared folder //CentOS7RDMA-HN/OpenFOAM onto the folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="fff14-235">O nome de usuário e a senha no comando devem ser o nome de usuário e a senha de um usuário de cluster no nó principal.</span><span class="sxs-lookup"><span data-stu-id="fff14-235">The username and password in the command should be the username and password of a cluster user on the head node.</span></span> <span data-ttu-id="fff14-236">(Confira [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx)).</span><span class="sxs-lookup"><span data-stu-id="fff14-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="fff14-237">O símbolo "\\`" no segundo comando é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fff14-237">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="fff14-238">"\\`," significa que "," (uma vírgula) é uma parte do comando.</span><span class="sxs-lookup"><span data-stu-id="fff14-238">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="fff14-239">Servidor NFS</span><span class="sxs-lookup"><span data-stu-id="fff14-239">NFS server</span></span>
<span data-ttu-id="fff14-240">O serviço NFS permite que você compartilhe e migre arquivos entre computadores com o sistema operacional Windows Server 2012 usando o protocolo SMB e computadores Linux usando o protocolo NFS.</span><span class="sxs-lookup"><span data-stu-id="fff14-240">The NFS service enables you to share and migrate files between computers running the Windows Server 2012 operating system using the SMB protocol and Linux-based computers using the NFS protocol.</span></span> <span data-ttu-id="fff14-241">O servidor NFS e todos os outros nós devem ser implantados na mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fff14-241">The NFS server and all other nodes have to be deployed in the same virtual network.</span></span> <span data-ttu-id="fff14-242">Ele fornece a melhor compatibilidade com nós do Linux em comparação com um compartilhamento SMB.</span><span class="sxs-lookup"><span data-stu-id="fff14-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="fff14-243">Por exemplo, ele dá suporte a links de arquivo.</span><span class="sxs-lookup"><span data-stu-id="fff14-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="fff14-244">Para instalar e configurar um servidor NFS, siga as etapas no [Servidor para primeiro compartilhamento do sistema de arquivos de rede ponta a ponta](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="fff14-244">To install and set up an NFS server, follow the steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="fff14-245">Por exemplo, crie um compartilhamento NFS chamado nfs com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="fff14-245">For example, create an NFS share named nfs with the following properties:</span></span>
   
    ![Autorização de NFS][nfsauth]
   
    ![Permissões de compartilhamento NFS][nfsshare]
   
    ![Permissões de compartilhamento NFS NTFS][nfsperm]
   
    ![Propriedades de gerenciamento de NFS][nfsmanage]
2. <span data-ttu-id="fff14-250">Abra uma janela do Windows PowerShell e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fff14-250">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="fff14-251">O primeiro comando cria uma pasta chamada /nfsshared em todos os nós do grupo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="fff14-251">The first command creates a folder named /nfsshared on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="fff14-252">O segundo comando monta o compartilhamento CentOS7RDMA-HN:/nfs para a pasta.</span><span class="sxs-lookup"><span data-stu-id="fff14-252">The second command mounts the NFS share CentOS7RDMA-HN:/nfs onto the folder.</span></span> <span data-ttu-id="fff14-253">Aqui, CentOS7RDMA-HN:/nfss é o caminho remoto do seu compartilhamento de NFS.</span><span class="sxs-lookup"><span data-stu-id="fff14-253">Here CentOS7RDMA-HN:/nfs is the remote path of your NFS share.</span></span>

## <a name="how-to-submit-jobs"></a><span data-ttu-id="fff14-254">Como enviar trabalhos</span><span class="sxs-lookup"><span data-stu-id="fff14-254">How to submit jobs</span></span>
<span data-ttu-id="fff14-255">Há várias maneiras de enviar trabalhos ao cluster HPC Pack:</span><span class="sxs-lookup"><span data-stu-id="fff14-255">There are several ways to submit jobs to the HPC Pack cluster:</span></span>

* <span data-ttu-id="fff14-256">Gerenciador de Cluster HPC ou GUI do Gerenciador de Trabalhos HPC</span><span class="sxs-lookup"><span data-stu-id="fff14-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="fff14-257">Portal da Web do HPC</span><span class="sxs-lookup"><span data-stu-id="fff14-257">HPC web portal</span></span>
* <span data-ttu-id="fff14-258">API REST</span><span class="sxs-lookup"><span data-stu-id="fff14-258">REST API</span></span>

<span data-ttu-id="fff14-259">O envio de trabalho para o cluster no Azure por meio de ferramentas de GUI do HPC Pack e o portal da Web do HPC são os mesmas para nós de computação do Windows.</span><span class="sxs-lookup"><span data-stu-id="fff14-259">Job submission to the cluster in Azure via HPC Pack GUI tools and the HPC web portal are the same as for Windows compute nodes.</span></span> <span data-ttu-id="fff14-260">Veja [Gerenciador de trabalhos do HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) e [Como enviar trabalhos de um computador cliente local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fff14-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How to submit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fff14-261">Para enviar trabalhos por meio da API REST, confira [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack (Windows HPC Server)](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="fff14-261">To submit jobs via the REST API, refer to [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="fff14-262">Para enviar trabalhos de um cliente Linux, consulte também o exemplo do Python no [SDK do HPC Pack](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="fff14-262">To submit jobs from a Linux client, also refer to the Python sample in the [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="fff14-263">Clusrun para nós Linux</span><span class="sxs-lookup"><span data-stu-id="fff14-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="fff14-264">A ferramenta [clusrun](https://technet.microsoft.com/library/cc947685.aspx) do HPC Pack pode ser usada para executar comandos em nós do Linux por meio de um Prompt de comando ou do Gerenciador de Cluster do HPC.</span><span class="sxs-lookup"><span data-stu-id="fff14-264">The HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used to execute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="fff14-265">Veja alguns exemplos básicos.</span><span class="sxs-lookup"><span data-stu-id="fff14-265">Following are some basic examples.</span></span>

* <span data-ttu-id="fff14-266">Mostre os nomes de usuário atuais em todos os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="fff14-266">Show current user names on all nodes in the cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="fff14-267">Instale a ferramenta de depuração **gdb** com o **yum** em todos os nós do grupo linuxnodes e os reinicie após 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="fff14-267">Install the **gdb** debugger tool with **yum** on all nodes in the linuxnodes group and then restart the nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="fff14-268">Crie um script de shell exibindo cada número de 1 a 10 durante um segundo em cada nó no cluster, execute-o e mostre imediatamente a saída dos nós.</span><span class="sxs-lookup"><span data-stu-id="fff14-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in the cluster, run it, and show output from the nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="fff14-269">Talvez seja necessário usar determinados caracteres de escape em comandos **clusrun** .</span><span class="sxs-lookup"><span data-stu-id="fff14-269">You might need to use certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="fff14-270">Como mostra este exemplo, use ^ em um Prompt de Comando para escapar o símbolo ">".</span><span class="sxs-lookup"><span data-stu-id="fff14-270">As shown in this example, use ^ in a Command Prompt to escape the ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fff14-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fff14-271">Next steps</span></span>
* <span data-ttu-id="fff14-272">Tente dimensionar verticalmente o cluster para um maior número de nós ou executar uma carga de trabalho do Linux no cluster.</span><span class="sxs-lookup"><span data-stu-id="fff14-272">Try scaling up the cluster to a larger number of nodes, or try running a Linux workload on the cluster.</span></span> <span data-ttu-id="fff14-273">Para ver um exemplo, confira [Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="fff14-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="fff14-274">Tente um cluster com [VMs compatíveis com RDMA, com uso intensivo de computação](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para executar cargas de trabalho MPI.</span><span class="sxs-lookup"><span data-stu-id="fff14-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to run MPI workloads.</span></span> <span data-ttu-id="fff14-275">Para ver um exemplo, confira [Executar o OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="fff14-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="fff14-276">Se você estiver interessado em trabalhar em nós do Linux em um cluster do HPC Pack local, veja as [diretrizes do TechNet](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="fff14-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see the [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
