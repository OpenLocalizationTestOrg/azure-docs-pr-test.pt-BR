---
title: "aaaLinux de computação VMs em um cluster de HPC Pack | Microsoft Docs"
description: "Saiba como toocreate e usar um pacote de HPC cluster no Azure para cargas de trabalho (HPC) de computação de alto e desempenho do Linux"
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
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="2e4cc-103">Introdução a nós de computação Linux em um cluster de HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="2e4cc-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="2e4cc-104">Configure um cluster do [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) no Azure que contenha um nó de cabeçalho que executa o Windows Server e vários nós de computação que executam uma distribuição do Linux com suporte.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="2e4cc-105">Explore opções toomove dados entre nós do Linux hello e o nó principal do Windows de saudação do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="2e4cc-106">Saiba como toosubmit Linux HPC trabalhos toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="2e4cc-107">Em um nível alto, hello diagrama a seguir mostra o cluster de HPC Pack Olá criar e trabalhar com.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Cluster HPC Pack com nós Linux][scenario]

<span data-ttu-id="2e4cc-109">Para outra opções toorun Linux HPC cargas de trabalho no Azure, consulte [recursos técnicos para o lote e computação de alto desempenho](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="2e4cc-110">Implantar um cluster de HPC Pack com nós de computação Linux</span><span class="sxs-lookup"><span data-stu-id="2e4cc-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="2e4cc-111">Este artigo mostra duas opções toodeploy um cluster de HPC Pack no Azure conosco de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="2e4cc-112">Ambos os métodos usam uma imagem do Marketplace do Windows Server com o nó principal do HPC Pack toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="2e4cc-113">**Modelo do Gerenciador de recursos do Azure** -usar um modelo de saudação do Azure Marketplace ou um modelo de início rápido da comunidade hello, tooautomate criação de cluster de saudação no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="2e4cc-114">Por exemplo, Olá [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modelo no hello Azure Marketplace cria uma infraestrutura completa de cluster de HPC Pack para Linux HPC cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="2e4cc-115">**Script do PowerShell** -Olá Use [script de implantação do Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-hpciaascluster.ps1**) tooautomate uma implantação completa de cluster no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="2e4cc-116">Este script do PowerShell do Azure usa uma imagem de VM do HPC Pack em hello Azure Marketplace para implantação rápida e fornece um conjunto abrangente de toodeploy de parâmetros de configuração de nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="2e4cc-117">Para obter mais informações sobre as opções de implantação de cluster de HPC Pack no Azure, consulte [opções toocreate e gerenciar um cluster de computação de alto desempenho (HPC) no Azure com Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2e4cc-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2e4cc-118">Prerequisites</span></span>
* <span data-ttu-id="2e4cc-119">**Assinatura do Azure** -você pode usar uma assinatura em qualquer serviço Global Azure ou Azure China hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="2e4cc-120">Se você não tem uma conta, pode criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="2e4cc-121">**Cota de núcleos** -você pode precisar de uma cota de Olá tooincrease de núcleos, especialmente se você escolher toodeploy vários nós de cluster com tamanhos VM com vários núcleos.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="2e4cc-122">tooincrease uma cota, abra uma solicitação de suporte do cliente online sem custo adicional.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="2e4cc-123">**Distribuições do Linux** -atualmente HPC Pack suporta Olá distribuições do Linux para nós de computação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="2e4cc-124">Você pode usar as versões do Marketplace dessas distribuições quando disponíveis ou fornecer as suas próprias.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="2e4cc-125">**Com base em centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, HPC 6.5, HPC 7.1</span><span class="sxs-lookup"><span data-stu-id="2e4cc-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="2e4cc-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="2e4cc-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="2e4cc-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 para HPC, SLES 12 para HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="2e4cc-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="2e4cc-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="2e4cc-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="2e4cc-129">rede de RDMA do Azure Olá toouse com um dos tamanhos de VM Olá compatíveis com RDMA, especifique uma imagem do SUSE Linux Enterprise Server 12 HPC ou com base em CentOS HPC de saudação do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="2e4cc-130">Para obter mais informações, consulte [Tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="2e4cc-131">Cluster de saudação pré-requisitos adicionais toodeploy usando o script de implantação de IaaS do HPC Pack hello:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="2e4cc-132">**Computador cliente** -você precisa de um script de implantação do cliente com base em Windows computador toorun Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="2e4cc-133">**Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="2e4cc-134">**Script de implantação IaaS do HPC Pack** - baixar e descompactar a versão mais recente de saudação do script Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="2e4cc-135">Você pode verificar a versão de saudação do script hello executando `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="2e4cc-136">Este artigo se baseia na versão 4.4.1 ou posterior do script hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="2e4cc-137">Opção de implantação 1.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-137">Deployment option 1.</span></span> <span data-ttu-id="2e4cc-138">Use um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e4cc-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="2e4cc-139">Vá toohello [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modelo no hello Azure Marketplace e clique em **implantar**.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="2e4cc-140">Olá portal do Azure, examinar as informações de saudação e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Criação de portal][portal]
3. <span data-ttu-id="2e4cc-142">Em Olá **Noções básicas sobre** folha, insira um nome para o cluster de saudação, que também nomeia a VM do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="2e4cc-143">Você pode escolher um grupo de recursos existente ou crie um grupo para a implantação de saudação em um local que é tooyou disponível.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="2e4cc-144">Hello local afeta a disponibilidade de saudação de determinados tamanhos de VM e outros serviços do Azure (consulte [produtos disponíveis por região](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="2e4cc-145">Em Olá **configurações do nó de cabeçalho** folha, para uma implantação primeiro, você pode aceitar as configurações padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2e4cc-146">Olá **script pós-configuração URL** é uma configuração opcional toospecify um script do Windows PowerShell publicamente disponível que você deseja toorun na VM do nó principal Olá depois que ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="2e4cc-147">Em Olá **configurações de nós de computação** folha, selecione um padrão de nomeação de nós hello, o número de saudação e o tamanho de nós de saudação e Olá toodeploy de distribuição do Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="2e4cc-148">Em Olá **definições de infraestrutura** folha, insira os nomes de rede virtual hello e Active Directory domínio, domínio e as credenciais de administrador VM e um padrão de nomeação para as contas de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2e4cc-149">HPC Pack usa os usuários de cluster tooauthenticate de domínio do Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="2e4cc-150">Depois de executar testes de validação de saudação e revise os termos de uso do hello, clique em **compra**.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="2e4cc-151">Opção de implantação 2.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-151">Deployment option 2.</span></span> <span data-ttu-id="2e4cc-152">Usar script de implantação IaaS Olá</span><span class="sxs-lookup"><span data-stu-id="2e4cc-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="2e4cc-153">Estes são os cluster de saudação toodeploy pré-requisitos adicionais usando o script de implantação de IaaS do HPC Pack Olá:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="2e4cc-154">**Computador cliente** -você precisa de um script de implantação do cliente com base em Windows computador toorun Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="2e4cc-155">**Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="2e4cc-156">**Script de implantação IaaS do HPC Pack** - baixar e descompactar a versão mais recente de saudação do script Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="2e4cc-157">Você pode verificar a versão de saudação do script hello executando `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="2e4cc-158">Este artigo se baseia na versão 4.4.1 ou posterior do script hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="2e4cc-159">**Arquivo de configuração XML**</span><span class="sxs-lookup"><span data-stu-id="2e4cc-159">**XML configuration file**</span></span>

<span data-ttu-id="2e4cc-160">Olá script de implantação IaaS do HPC Pack usa um arquivo de configuração XML como cluster HPC Olá toodescribe de entrada.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="2e4cc-161">Olá seguinte arquivo de configuração de exemplo especifica um pequeno cluster consiste em um nó principal do HPC Pack e dois nós de computação do tamanho A7 CentOS 7.0 Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="2e4cc-162">Modificar arquivo hello conforme necessário para seu ambiente e a configuração de cluster desejado e salve-o com um nome como HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="2e4cc-163">Por exemplo, você precisa toosupply nome da sua assinatura e um nome de conta de armazenamento exclusivo e o nome do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="2e4cc-164">Além disso, talvez você queira toochoose outro suporte para a imagem do Linux para nós de computação hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="2e4cc-165">Para obter mais informações sobre elementos Olá no arquivo de configuração hello, consulte o arquivo de Manual.rtf Olá na pasta de script hello e [criar um cluster HPC com hello script de implantação IaaS do HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="2e4cc-166">**Olá toorun script de implantação IaaS do HPC Pack**</span><span class="sxs-lookup"><span data-stu-id="2e4cc-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="2e4cc-167">Abra o Windows PowerShell como administrador no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="2e4cc-168">Alterar pasta de toohello de diretório em que o script hello está instalado (E:\IaaSClusterScript neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="2e4cc-169">Execute Olá cluster de HPC Pack de saudação do comando toodeploy a seguir.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="2e4cc-170">Este exemplo supõe que esse arquivo de configuração hello está localizado em E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="2e4cc-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="2e4cc-171">a.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-171">a.</span></span> <span data-ttu-id="2e4cc-172">Porque Olá **AdminPassword** não for especificado Olá antes do comando, você é tooenter solicitadas senha de saudação do usuário *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="2e4cc-173">b.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-173">b.</span></span> <span data-ttu-id="2e4cc-174">script Hello, em seguida, inicia o arquivo de configuração toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="2e4cc-175">Pode demorar até tooseveral minutos dependendo da conexão de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Validação][validate]
   
    <span data-ttu-id="2e4cc-177">c.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-177">c.</span></span> <span data-ttu-id="2e4cc-178">Depois de passarem validações, script hello lista Olá toocreate de recursos de cluster.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="2e4cc-179">Digite *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-179">Enter *Y* toocontinue.</span></span>
   
    ![Recursos][resources]
   
    <span data-ttu-id="2e4cc-181">d.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-181">d.</span></span> <span data-ttu-id="2e4cc-182">script Hello inicia o cluster de HPC Pack toodeploy hello e conclui a configuração de saudação sem mais etapas manuais.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="2e4cc-183">Olá script pode ser executado por vários minutos.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-183">hello script can run for several minutes.</span></span>
   
    ![Implantar][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="2e4cc-185">Neste exemplo, script hello gera um arquivo de log automaticamente desde Olá **- arquivo de log** parâmetro não for especificado.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="2e4cc-186">Olá logs não são gravados em tempo real, mas são coletados no final de saudação de validação de saudação e implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="2e4cc-187">Se Olá PowerShell processo for interrompido enquanto o script hello está sendo executado, alguns logs serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="2e4cc-188">Conecte-se o nó principal toohello</span><span class="sxs-lookup"><span data-stu-id="2e4cc-188">Connect toohello head node</span></span>
<span data-ttu-id="2e4cc-189">Depois de implantar o cluster de HPC Pack Olá no Azure, [conectar por área de trabalho remota](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nó principal VM usando Olá credenciais de domínio fornecido quando você implantou o cluster hello (por exemplo, *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="2e4cc-190">Você gerencia o cluster de saudação do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="2e4cc-191">No nó de cabeçalho hello, inicie toocheck do Gerenciador de Cluster de HPC status de saudação do cluster de HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="2e4cc-192">Você pode gerenciar e monitorar nós de computação Linux hello mesma maneira que trabalha com o Windows nós de computação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="2e4cc-193">Por exemplo, você verá que nós do Linux Olá listados no **gerenciamento de recursos** (esses nós são implantados com hello **LinuxNode** modelo).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Gerenciamento de nós][management]

<span data-ttu-id="2e4cc-195">Você também ver nós Linux Olá Olá **mapa de calor** exibição.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Mapa de calor][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="2e4cc-197">Como toomove dados em um cluster conosco do Linux</span><span class="sxs-lookup"><span data-stu-id="2e4cc-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="2e4cc-198">Você tem vários dados de toomove opções entre nós do Linux e o nó principal do Windows de saudação do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="2e4cc-199">Aqui estão os três métodos comuns, descritos mais detalhadamente Olá seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="2e4cc-200">**Arquivo do Azure** -expõe um toostore dados gerenciados do SMB arquivo compartilhamento de arquivos no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="2e4cc-201">Nós do Windows e Linux pode montar um compartilhamento de arquivos do Azure como uma unidade ou pasta em Olá a mesma hora, mesmo se eles são implantados em redes virtuais diferentes.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="2e4cc-202">**Nó de cabeçalho SMB compartilhar** -monta uma pasta compartilhada do Windows padrão do nó principal Olá em nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="2e4cc-203">**Servidor NFS do nó de cabeçalho** – fornece uma solução de compartilhamento de arquivos para um ambiente misto do Windows e do Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="2e4cc-204">Armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="2e4cc-204">Azure File storage</span></span>
<span data-ttu-id="2e4cc-205">Olá [arquivo Azure](https://azure.microsoft.com/services/storage/files/) serviço expõe os compartilhamentos de arquivos usando o protocolo SMB 2.1 padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="2e4cc-206">Serviços de nuvem e VMs do Azure podem compartilhar dados de arquivo entre componentes de aplicativos por meio de compartilhamentos montados e aplicativos locais podem acessar dados de arquivo em um compartilhamento de por meio de saudação API de armazenamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="2e4cc-207">Para etapas detalhadas toocreate um arquivo do Azure compartilham e recriá-lo no nó de cabeçalho hello, consulte [Introdução ao armazenamento de arquivo do Azure no Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="2e4cc-208">compartilhamento de arquivo do Azure Olá toomount em nós do Linux hello, consulte [como toouse armazenamento de arquivo do Azure com Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="2e4cc-209">tooset as conexões persistentes, consulte [Persisting conexões tooMicrosoft arquivos do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="2e4cc-210">Em Olá exemplo a seguir, crie um compartilhamento de arquivos do Azure em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="2e4cc-211">Olá toomount compartilhamento no nó principal hello, abra um Prompt de comando e digite Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="2e4cc-212">Neste exemplo, allvhdsje é o nome da sua conta de armazenamento, storageaccountkey é a chave da conta de armazenamento e o rdma é o nome de compartilhamento de arquivo do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="2e4cc-213">compartilhamento de arquivo do Azure Olá está montado como z no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="2e4cc-214">compartilhamento de arquivo do Azure Olá toomount em nós do Linux, execute um **clusrun** comando no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="2e4cc-215">**[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  é um toocarry de ferramenta do HPC Pack útil tarefas administrativas em vários nós.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="2e4cc-216">(Consulte também [Clusrun para nós Linux](#Clusrun-for-Linux-nodes) neste artigo.)</span><span class="sxs-lookup"><span data-stu-id="2e4cc-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="2e4cc-217">Abra uma janela do Windows PowerShell e digite Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="2e4cc-218">Olá primeiro comando cria uma pasta chamada /rdma em todos os nós no grupo de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="2e4cc-219">comando segundo Olá monta hello Azure arquivo compartilhamento allvhdsjw.file.core.windows.net/rdma para pasta de /rdma Olá com too777 de conjunto de bits modo dir e arquivo.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="2e4cc-220">No segundo comando de hello, allvhdsje é o nome da sua conta de armazenamento e storageaccountkey é a chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="2e4cc-221">Olá "\\`" símbolo no segundo comando de saudação é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="2e4cc-222">"\\`,"significa que hello"," (vírgula) é uma parte do comando hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="2e4cc-223">Compartilhamento do nó principal</span><span class="sxs-lookup"><span data-stu-id="2e4cc-223">Head node share</span></span>
<span data-ttu-id="2e4cc-224">Como alternativa, monte uma pasta compartilhada de nó principal Olá em nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="2e4cc-225">Um compartilhamento fornece arquivos de tooshare de maneira mais simples do hello, mas nó principal hello e todos os nós do Linux devem ser implantados em Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="2e4cc-226">Aqui estão as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-226">Here are hello steps.</span></span>

1. <span data-ttu-id="2e4cc-227">Crie uma pasta no nó principal hello e compartilhá-lo tooEveryone com permissões de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="2e4cc-228">Por exemplo, compartilhar D:\OpenFOAM no nó principal do hello como \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="2e4cc-229">Aqui HN CentOS7RDMA é o nome de host de saudação do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Permissões de compartilhamento de arquivo][fileshareperms]
   
    ![Compartilhamento de arquivos][filesharing]
2. <span data-ttu-id="2e4cc-232">Abra uma janela do Windows PowerShell e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="2e4cc-233">Olá primeiro comando cria uma pasta chamada /openfoam em todos os nós no grupo de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="2e4cc-234">comando segundo Olá monta Olá compartilhado pasta //CentOS7RDMA-HN/OpenFOAM na pasta Olá com dir e arquivo too777 de conjunto de bits de modo.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="2e4cc-235">Olá username e password no comando Olá devem ser Olá nome de usuário e senha de um usuário de cluster no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="2e4cc-236">(Confira [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="2e4cc-237">Olá "\\`" símbolo no segundo comando de saudação é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="2e4cc-238">"\\`,"significa que hello"," (vírgula) é uma parte do comando hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="2e4cc-239">Servidor NFS</span><span class="sxs-lookup"><span data-stu-id="2e4cc-239">NFS server</span></span>
<span data-ttu-id="2e4cc-240">Olá serviço NFS permite tooshare e migra arquivos entre computadores que executam o sistema operacional de saudação do Windows Server 2012 usando o protocolo SMB de saudação e computadores baseados em Linux usando o protocolo NFS de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="2e4cc-241">Olá servidor NFS e todos os outros nós têm toobe implantado em Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="2e4cc-242">Ele fornece a melhor compatibilidade com nós do Linux em comparação com um compartilhamento SMB.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="2e4cc-243">Por exemplo, ele dá suporte a links de arquivo.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="2e4cc-244">tooinstall e configurar um servidor NFS, siga as etapas de saudação em [servidor para compartilhamento primeiro do sistema de arquivos de rede ponta a ponta](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="2e4cc-245">Por exemplo, crie um compartilhamento NFS chamado nfs com hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![Autorização de NFS][nfsauth]
   
    ![Permissões de compartilhamento NFS][nfsshare]
   
    ![Permissões de compartilhamento NFS NTFS][nfsperm]
   
    ![Propriedades de gerenciamento de NFS][nfsmanage]
2. <span data-ttu-id="2e4cc-250">Abra uma janela do Windows PowerShell e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="2e4cc-251">Olá primeiro comando cria uma pasta chamada /nfsshared em todos os nós no grupo de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="2e4cc-252">saudação de montagens segundo comando NFS Hello compartilhar HN CentOS7RDMA: / nfs em Olá pasta.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="2e4cc-253">Aqui CentOS7RDMA HN: nfs é o caminho remoto de saudação do seu compartilhamento NFS.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="2e4cc-254">Como toosubmit trabalhos</span><span class="sxs-lookup"><span data-stu-id="2e4cc-254">How toosubmit jobs</span></span>
<span data-ttu-id="2e4cc-255">Há um cluster de HPC Pack do várias maneiras toosubmit trabalhos toohello:</span><span class="sxs-lookup"><span data-stu-id="2e4cc-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="2e4cc-256">Gerenciador de Cluster HPC ou GUI do Gerenciador de Trabalhos HPC</span><span class="sxs-lookup"><span data-stu-id="2e4cc-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="2e4cc-257">Portal da Web do HPC</span><span class="sxs-lookup"><span data-stu-id="2e4cc-257">HPC web portal</span></span>
* <span data-ttu-id="2e4cc-258">API REST</span><span class="sxs-lookup"><span data-stu-id="2e4cc-258">REST API</span></span>

<span data-ttu-id="2e4cc-259">Envio de trabalho cluster toohello no Azure por meio de ferramentas de GUI do HPC Pack e o portal da web hello HPC estão Olá mesmo para nós de computação do Windows.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="2e4cc-260">Consulte [Gerenciador de trabalhos do HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) e [como toosubmit trabalhos de um computador de cliente local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2e4cc-261">trabalhos toosubmit via Olá API REST, consulte muito[criando e enviando trabalhos usando Olá API REST do Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="2e4cc-262">toosubmit trabalhos de um cliente do Linux, consulte exemplo de Python toohello Olá também [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="2e4cc-263">Clusrun para nós Linux</span><span class="sxs-lookup"><span data-stu-id="2e4cc-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="2e4cc-264">Olá HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) ferramenta pode ser usada tooexecute comandos em nós do Linux por meio de um Prompt de comando ou o Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="2e4cc-265">Veja alguns exemplos básicos.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-265">Following are some basic examples.</span></span>

* <span data-ttu-id="2e4cc-266">Mostre nomes de usuário atuais em todos os nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="2e4cc-267">Instalar Olá **gdb** ferramenta de depuração com **yum** em todos os nós Olá linuxnodes grupo e, em seguida, reinicie nós de saudação após 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="2e4cc-268">Criar um script de shell exibindo cada número de 1 a 10 para um segundo em cada nó do Linux no cluster hello, executá-lo e Mostrar saída de nós Olá imediatamente.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="2e4cc-269">Talvez seja necessário toouse certos caracteres de escape **clusrun** comandos.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="2e4cc-270">Conforme mostrado neste exemplo, usar ^ em uma saudação do Prompt de comando tooescape ">" símbolo.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2e4cc-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e4cc-271">Next steps</span></span>
* <span data-ttu-id="2e4cc-272">Tente expansão Olá cluster tooa maior número de nós, ou executando uma carga de trabalho do Linux no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="2e4cc-273">Para ver um exemplo, confira [Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="2e4cc-274">Tente um cluster com [compatíveis com RDMA, com uso intensivo de computação VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun cargas de trabalho MPI.</span><span class="sxs-lookup"><span data-stu-id="2e4cc-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="2e4cc-275">Para ver um exemplo, confira [Executar o OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="2e4cc-276">Se você estiver interessado em trabalhar com nós do Linux em um cluster de HPC Pack no local, consulte Olá [orientação da TechNet](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e4cc-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

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
