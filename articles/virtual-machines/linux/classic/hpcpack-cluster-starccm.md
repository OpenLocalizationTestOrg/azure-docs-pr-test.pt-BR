---
title: Executar o STAR-CCM+ com o HPC Pack em VMs do Linux | Microsoft Docs
description: "Implante um cluster do Microsoft HPC Pack no Azure e execute um trabalho do STAR-CCM+ em vários nós de computação do Linux em uma rede RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: b45fcfb981287035da02fda62eaf5f9436ec2379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="4aa62-103">Executar o STAR-CCM+ com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="4aa62-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="4aa62-104">Este artigo mostra como implantar um cluster do Microsoft HPC Pack no Azure e executar um trabalho do [STAR-CCM+ da CD-adapco](http://www.cd-adapco.com/products/star-ccm%C2%AE) em vários nós de computação Linux interconectados com InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="4aa62-104">This article shows you how to deploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="4aa62-105">O Microsoft HPC Pack fornece recursos para executar uma variedade de aplicativos de HPC e paralelos em larga escala, incluindo aplicativos MPI, em clusters de máquinas virtuais do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa62-105">Microsoft HPC Pack provides features to run a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="4aa62-106">O HPC Pack também dá suporte à execução de aplicativos de HPC do Linux em VMs com nós de computação do Linux implantadas em um cluster do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4aa62-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="4aa62-107">Para saber como começar a usar os nós de computação do Linux com o HPC Pack, consulte a [Introdução a nós de computação Linux em um cluster HPC Pack no Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4aa62-107">For an introduction to using Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="4aa62-108">Configurar um cluster do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="4aa62-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="4aa62-109">Baixe os scripts de implantação de IaaS do HPC Pack do [Centro de Download](https://www.microsoft.com/en-us/download/details.aspx?id=44949) e extraia-os localmente.</span><span class="sxs-lookup"><span data-stu-id="4aa62-109">Download the HPC Pack IaaS deployment scripts from the [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="4aa62-110">O Azure PowerShell é um pré-requisito.</span><span class="sxs-lookup"><span data-stu-id="4aa62-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="4aa62-111">Se o PowerShell não estiver configurado no computador local, leia [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4aa62-111">If PowerShell is not configured on your local machine, please read the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="4aa62-112">No momento da redação deste artigo, as imagens do Linux do Azure Marketplace (que contém os drivers de InfiniBand para o Azure) são para o SLES 12, o CentOS 6.5 e o CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="4aa62-112">At the time of this writing, the Linux images from the Azure Marketplace (which contains the InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="4aa62-113">Este artigo baseia-se no uso do SLES 12.</span><span class="sxs-lookup"><span data-stu-id="4aa62-113">This article is based on the usage of SLES 12.</span></span> <span data-ttu-id="4aa62-114">Para recuperar o nome de todas as imagens do Linux que dão suporte ao HPC no Marketplace, você pode executar o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4aa62-114">To retrieve the name of all Linux images that support HPC in the Marketplace, you can run the following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="4aa62-115">A saída lista o local em que essas imagens estão disponíveis e o nome da imagem (**ImageName**) a ser usado no modelo de implantação posteriormente.</span><span class="sxs-lookup"><span data-stu-id="4aa62-115">The output lists the location in which these images are available and the image name (**ImageName**) to be used in the deployment template later.</span></span>

<span data-ttu-id="4aa62-116">Antes de implantar o cluster, você precisa criar um arquivo de modelo de implantação do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4aa62-116">Before you deploy the cluster, you have to build an HPC Pack deployment template file.</span></span> <span data-ttu-id="4aa62-117">Como nosso alvo é um cluster pequeno, o nó principal será o controlador de domínio e hospedará um banco de dados SQL local.</span><span class="sxs-lookup"><span data-stu-id="4aa62-117">Because we're targeting a small cluster, the head node will be the domain controller and host a local SQL database.</span></span>

<span data-ttu-id="4aa62-118">O modelo a seguir implantará esse nó de cabeçalho, criará um arquivo XML chamado **MyCluster.xml** e substituirá os valores de **SubscriptionId**, **StorageAccount**, **Location**, **VMName** e **ServiceName** pelos seus.</span><span class="sxs-lookup"><span data-stu-id="4aa62-118">The following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace the values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="4aa62-119">Inicie a criação do nó principal executando o comando do PowerShell em um prompt de comandos com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="4aa62-119">Start the head-node creation by running the PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="4aa62-120">Após 20 a 30 minutos, o nó principal deverá estar pronto.</span><span class="sxs-lookup"><span data-stu-id="4aa62-120">After 20 to 30 minutes, the head node should be ready.</span></span> <span data-ttu-id="4aa62-121">Você pode se conectar a ele do portal do Azure clicando no ícone **Conectar** da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4aa62-121">You can connect to it from the Azure portal by clicking the **Connect** icon of the virtual machine.</span></span>

<span data-ttu-id="4aa62-122">Eventualmente, talvez você precise consertar o encaminhador DNS.</span><span class="sxs-lookup"><span data-stu-id="4aa62-122">You might eventually have to fix the DNS forwarder.</span></span> <span data-ttu-id="4aa62-123">Para fazer isso, inicie o Gerenciador DNS.</span><span class="sxs-lookup"><span data-stu-id="4aa62-123">To do so, start DNS Manager.</span></span>

1. <span data-ttu-id="4aa62-124">Clique com o botão direito do mouse no nome do servidor no Gerenciador DNS, selecione **Propriedades** e clique na guia **Encaminhadores**.</span><span class="sxs-lookup"><span data-stu-id="4aa62-124">Right-click the server name in DNS Manager, select **Properties**, and then click the **Forwarders** tab.</span></span>
2. <span data-ttu-id="4aa62-125">Clique no botão **Editar** para remover quaisquer encaminhadores e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4aa62-125">Click the **Edit** button to remove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="4aa62-126">Certifique-se de que a caixa de seleção **Usar dicas de raiz se encaminhadores não estiverem disponíveis** esteja marcada e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4aa62-126">Make sure that the **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="4aa62-127">Configurar nós de computação do Linux</span><span class="sxs-lookup"><span data-stu-id="4aa62-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="4aa62-128">Você implanta os nós de computação do Linux usando o mesmo modelo de implantação que usou para criar o nó principal.</span><span class="sxs-lookup"><span data-stu-id="4aa62-128">You deploy the Linux compute nodes by using the same deployment template that you used to create the head node.</span></span>

<span data-ttu-id="4aa62-129">Copie o arquivo **MyCluster.xml** do computador local para o nó de cabeçalho e atualize a marcação **NodeCount** com o número de nós que você deseja implantar (<=20).</span><span class="sxs-lookup"><span data-stu-id="4aa62-129">Copy the file **MyCluster.xml** from your local machine to the head node, and update the **NodeCount** tag with the number of nodes that you want to deploy (<=20).</span></span> <span data-ttu-id="4aa62-130">Tenha cuidado para ter núcleos suficientes disponíveis na sua cota do Azure, porque cada instância A9 consumirá 16 núcleos de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="4aa62-130">Be careful to have enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="4aa62-131">Você poderá usar instâncias A8 (8 núcleos) em vez de A9 se quiser usar mais VMs no mesmo orçamento.</span><span class="sxs-lookup"><span data-stu-id="4aa62-131">You can use A8 instances (8 cores) instead of A9 if you want to use more VMs in the same budget.</span></span>

<span data-ttu-id="4aa62-132">No nó principal, copie os scripts de implantação de IaaS do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4aa62-132">On the head node, copy the HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="4aa62-133">Execute os seguintes comandos do Azure PowerShell em um prompt de comandos com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="4aa62-133">Run the following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="4aa62-134">Execute **Add-AzureAccount** para se conectar à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa62-134">Run **Add-AzureAccount** to connect to your Azure subscription.</span></span>
2. <span data-ttu-id="4aa62-135">Se tiver várias assinaturas, execute **Get-AzureSubscription** para listá-las.</span><span class="sxs-lookup"><span data-stu-id="4aa62-135">If you have multiple subscriptions, run **Get-AzureSubscription** to list them.</span></span>
3. <span data-ttu-id="4aa62-136">Defina uma assinatura padrão executando o comando **Select-AzureSubscription -SubscriptionName xxxx -Default** .</span><span class="sxs-lookup"><span data-stu-id="4aa62-136">Set a default subscription by running the **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="4aa62-137">Execute **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** para iniciar a implantação dos nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="4aa62-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** to start deploying Linux compute nodes.</span></span>
   
   ![Implantação do nó principal em ação][hndeploy]

<span data-ttu-id="4aa62-139">Abra a ferramenta de Gerenciador de Cluster do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4aa62-139">Open the HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="4aa62-140">Após alguns minutos, os nós de computação do Linux aparecerão regularmente na lista de nós de computação do cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa62-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="4aa62-141">Com o modo de implantação clássico, as VMs de IaaS são criadas em sequência.</span><span class="sxs-lookup"><span data-stu-id="4aa62-141">With the classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="4aa62-142">Sendo assim, se o número de nós for importante, fazer com que todas elas sejam implantadas poderá levar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="4aa62-142">So if the number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Nós do Linux no Gerenciador de Cluster do HPC Pack][clustermanager]

<span data-ttu-id="4aa62-144">Agora que todos os nós estão em funcionamento, há configurações de infraestrutura adicionais a serem definidas.</span><span class="sxs-lookup"><span data-stu-id="4aa62-144">Now that all nodes are up and running in the cluster, there are additional infrastructure settings to make.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="4aa62-145">Configurar um compartilhamento de arquivos do Azure para nós do Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="4aa62-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="4aa62-146">Você pode usar o serviço de arquivos do Azure para armazenar scripts, pacotes de aplicativos e arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="4aa62-146">You can use the Azure File service to store scripts, application packages, and data files.</span></span> <span data-ttu-id="4aa62-147">O arquivo do Azure fornece funcionalidades CIFS sobre o Armazenamento de Blobs do Azure como um repositório persistente.</span><span class="sxs-lookup"><span data-stu-id="4aa62-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="4aa62-148">Lembre-se de que essa não é a solução mais escalonável, mas é a mais simples e não requer VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="4aa62-148">Be aware that this is not the most scalable solution, but it is the simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="4aa62-149">Crie um compartilhamento de arquivos do Azure seguindo as instruções no artigo [Introdução ao Armazenamento de Arquivos do Azure no Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="4aa62-149">Create an Azure File share by following the instructions in the article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="4aa62-150">Mantenha o nome da sua conta de armazenamento como **saname**, o nome do compartilhamento de arquivos como **sharename** e a chave de conta de armazenamento **sakey**.</span><span class="sxs-lookup"><span data-stu-id="4aa62-150">Keep the name of your storage account as **saname**, the file share name as **sharename**, and the storage account key as **sakey**.</span></span>

### <a name="mount-the-azure-file-share-on-the-head-node"></a><span data-ttu-id="4aa62-151">Montar o compartilhamento de arquivos do Azure no nó principal</span><span class="sxs-lookup"><span data-stu-id="4aa62-151">Mount the Azure File share on the head node</span></span>
<span data-ttu-id="4aa62-152">Abra um prompt de comandos com privilégios elevados e execute o seguinte comando para armazenar as credenciais no cofre do computador local:</span><span class="sxs-lookup"><span data-stu-id="4aa62-152">Open an elevated command prompt and run the following command to store the credentials in the local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="4aa62-153">Em seguida, para montar o compartilhamento de arquivos do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="4aa62-153">Then, to mount the Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-the-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="4aa62-154">Montar o compartilhamento de arquivos do Azure em nós de computação do Linux</span><span class="sxs-lookup"><span data-stu-id="4aa62-154">Mount the Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="4aa62-155">Uma ferramenta útil que é fornecida com o HPC Pack é a ferramenta clusrun.</span><span class="sxs-lookup"><span data-stu-id="4aa62-155">One useful tool that comes with HPC Pack is the clusrun tool.</span></span> <span data-ttu-id="4aa62-156">Você pode usar essa ferramenta de linha de comando para executar o mesmo comando simultaneamente em um conjunto de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="4aa62-156">You can use this command-line tool to run the same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="4aa62-157">Em nosso caso, ela é usada para montar o compartilhamento de arquivos do Azure e fazer com que ele persista e sobreviva a reinicializações.</span><span class="sxs-lookup"><span data-stu-id="4aa62-157">In our case, it's used to mount the Azure File share and persist it to survive reboots.</span></span>
<span data-ttu-id="4aa62-158">Em um prompt de comandos com privilégios elevados no nó principal, execute os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4aa62-158">In an elevated command prompt on the head node, run the following commands.</span></span>

<span data-ttu-id="4aa62-159">Para criar o diretório de montagem:</span><span class="sxs-lookup"><span data-stu-id="4aa62-159">To create the mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="4aa62-160">Para montar o compartilhamento de arquivos do Azure:</span><span class="sxs-lookup"><span data-stu-id="4aa62-160">To mount the Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="4aa62-161">Para fazer com que o compartilhamento de montagem persista:</span><span class="sxs-lookup"><span data-stu-id="4aa62-161">To persist the mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="4aa62-162">Instalar o STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="4aa62-162">Install STAR-CCM+</span></span>
<span data-ttu-id="4aa62-163">As instâncias de VM do Azure A8 e A9 dão suporte ao InfiniBand e funcionalidades de RDMA.</span><span class="sxs-lookup"><span data-stu-id="4aa62-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="4aa62-164">Os drivers de kernel que habilitam essas funcionalidades estão disponíveis para imagens do Windows Server 2012 R2, SUSE 12, CentOS 6.5 e CentOS 7.1 no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4aa62-164">The kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in the Azure Marketplace.</span></span> <span data-ttu-id="4aa62-165">O Microsoft MPI e Intel MPI (versão 5. x) são as duas bibliotecas de MPI que dão suporte a esses drivers no Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa62-165">Microsoft MPI and Intel MPI (release 5.x) are the two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="4aa62-166">O STAR-CCM+ da CD-adapco versão 11.x e posterior é fornecido com o Intel MPI versão 5.x, portanto o suporte do InfiniBand para Azure está incluído.</span><span class="sxs-lookup"><span data-stu-id="4aa62-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="4aa62-167">Obter o pacote Linux64 do STAR-CCM+ no [portal do CD-adapco](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="4aa62-167">Get the Linux64 STAR-CCM+ package from the [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="4aa62-168">Em nosso caso, usamos a versão 11.02.010 com precisão mista.</span><span class="sxs-lookup"><span data-stu-id="4aa62-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="4aa62-169">No nó de cabeçalho, no compartilhamento de arquivos do Azure **/hpcdata**, crie um script de shell chamado **setupstarccm.sh** com o conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4aa62-169">On the head node, in the **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with the following content.</span></span> <span data-ttu-id="4aa62-170">Esse script será executado em cada nó de computação para configurar o STAR-CCM+ localmente.</span><span class="sxs-lookup"><span data-stu-id="4aa62-170">This script will be run on each compute node to set up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="4aa62-171">Script setupstarcm.sh de exemplo</span><span class="sxs-lookup"><span data-stu-id="4aa62-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh to set up STAR-CCM+ locally

    # Create the CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy the STAR-CCM package from the file share to the local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract the package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without the FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="4aa62-172">Agora, para instalar o STAR-CCM+ em todos os seus nós de computação do Linux, abra um prompt de comandos com privilégios elevados e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4aa62-172">Now, to set up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run the following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="4aa62-173">Enquanto o comando é executado, você pode monitorar o uso da CPU com o mapa de calor do Gerenciador de Cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa62-173">While the command is running, you can monitor the CPU usage by using the heat map of Cluster Manager.</span></span> <span data-ttu-id="4aa62-174">Depois de alguns minutos, todos os nós devem estar instalados corretamente.</span><span class="sxs-lookup"><span data-stu-id="4aa62-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="4aa62-175">Executar trabalhos do STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="4aa62-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="4aa62-176">O HPC Pack é usado por suas funcionalidades de agendador de trabalho para executar trabalhos do STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="4aa62-176">HPC Pack is used for its job scheduler capabilities in order to run STAR-CCM+ jobs.</span></span> <span data-ttu-id="4aa62-177">Para fazer isso, precisamos do suporte de alguns scripts que são usados para iniciar o trabalho e executar o STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="4aa62-177">To do so, we need the support of a few scripts that are used to start the job and run STAR-CCM+.</span></span> <span data-ttu-id="4aa62-178">Os dados de entrada são mantidos no compartilhamento de arquivos do Azure primeiro por questões de simplicidade.</span><span class="sxs-lookup"><span data-stu-id="4aa62-178">The input data is kept on the Azure File share first for simplicity.</span></span>

<span data-ttu-id="4aa62-179">O script do PowerShell a seguir é usado para enfileirar um trabalho do STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="4aa62-179">The following PowerShell script is used to queue a STAR-CCM+ job.</span></span> <span data-ttu-id="4aa62-180">Ele usa três argumentos:</span><span class="sxs-lookup"><span data-stu-id="4aa62-180">It takes three arguments:</span></span>

* <span data-ttu-id="4aa62-181">O nome do modelo</span><span class="sxs-lookup"><span data-stu-id="4aa62-181">The model name</span></span>
* <span data-ttu-id="4aa62-182">O número de nós a ser usado</span><span class="sxs-lookup"><span data-stu-id="4aa62-182">The number of nodes to be used</span></span>
* <span data-ttu-id="4aa62-183">O número de núcleos em cada nó a ser usado</span><span class="sxs-lookup"><span data-stu-id="4aa62-183">The number of cores on each node to be used</span></span>

<span data-ttu-id="4aa62-184">Como o STAR-CCM+ pode ocupar a largura de banda da memória, normalmente é melhor usar menos núcleos por nó de computação e adicionar novos nós.</span><span class="sxs-lookup"><span data-stu-id="4aa62-184">Because STAR-CCM+ can fill the memory bandwidth, it's usually better to use fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="4aa62-185">O número exato de núcleos por nó dependerá da família de processadores e da velocidade da interconexão.</span><span class="sxs-lookup"><span data-stu-id="4aa62-185">The exact number of cores per node will depend on the processor family and the interconnect speed.</span></span>

<span data-ttu-id="4aa62-186">Os nós são alocados exclusivamente para o trabalho e não podem ser compartilhados com outros trabalhos.</span><span class="sxs-lookup"><span data-stu-id="4aa62-186">The nodes are allocated exclusively for the job and can’t be shared with other jobs.</span></span> <span data-ttu-id="4aa62-187">O trabalho não será iniciado como um trabalho de MPI diretamente.</span><span class="sxs-lookup"><span data-stu-id="4aa62-187">The job is not started as an MPI job directly.</span></span> <span data-ttu-id="4aa62-188">O script de shell **runstarccm.sh** iniciará o iniciador de MPI.</span><span class="sxs-lookup"><span data-stu-id="4aa62-188">The **runstarccm.sh** shell script will start the MPI launcher.</span></span>

<span data-ttu-id="4aa62-189">O modelo de entrada e o script **runstarccm.sh** são armazenados no compartilhamento **/hpcdata** que foi montado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4aa62-189">The input model and the **runstarccm.sh** script are stored in the **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="4aa62-190">Os arquivos de log são nomeados com a ID do trabalho e são armazenados no **compartilhamento /hpcdata**, assim como os arquivos de saída do STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="4aa62-190">Log files are named with the job ID and are stored in the **/hpcdata share**, along with the STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="4aa62-191">Script SubmitStarccmJob.ps1 de exemplo</span><span class="sxs-lookup"><span data-stu-id="4aa62-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us the job ID that's used to identify the name of the uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit the job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="4aa62-192">Substitua **runner.java** por seu código de registro em log e código do iniciador de modelo Java do STAR-CCM+ preferidos.</span><span class="sxs-lookup"><span data-stu-id="4aa62-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="4aa62-193">Script runstarccm.sh de exemplo</span><span class="sxs-lookup"><span data-stu-id="4aa62-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # The path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set the mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into the hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with the hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="4aa62-194">Em nosso teste, usamos um token de licença do tipo Power-On-Demand.</span><span class="sxs-lookup"><span data-stu-id="4aa62-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="4aa62-195">Para esse token, você precisa definir a variável de ambiente **$CDLMD_LICENSE_FILE** como **1999@flex.cd-adapco.com** e a chave na opção **-podkey** da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="4aa62-195">For that token, you have to set the **$CDLMD_LICENSE_FILE** environment variable to **1999@flex.cd-adapco.com** and the key in the **-podkey** option of the command line.</span></span>

<span data-ttu-id="4aa62-196">Após a inicialização, o script extrai – das variáveis de ambiente definidas pelo HPC Pack **$CCP_NODES_CORES** – a lista de nós para criar um arquivo de host usado pelo iniciador de MPI.</span><span class="sxs-lookup"><span data-stu-id="4aa62-196">After some initialization, the script extracts--from the **$CCP_NODES_CORES** environment variables that HPC Pack set--the list of nodes to build a hostfile that the MPI launcher uses.</span></span> <span data-ttu-id="4aa62-197">Esse arquivo de host conterá a lista de nomes dos nós de computação que são usados para o trabalho, um nome por linha.</span><span class="sxs-lookup"><span data-stu-id="4aa62-197">This hostfile will contain the list of compute node names that are used for the job, one name per line.</span></span>

<span data-ttu-id="4aa62-198">O formato **$CCP_NODES_CORES** segue este padrão:</span><span class="sxs-lookup"><span data-stu-id="4aa62-198">The format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="4aa62-199">Em que:</span><span class="sxs-lookup"><span data-stu-id="4aa62-199">Where:</span></span>

* <span data-ttu-id="4aa62-200">`<Number of nodes>` é o número de nós alocados para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="4aa62-200">`<Number of nodes>` is the number of nodes allocated to this job.</span></span>
* <span data-ttu-id="4aa62-201">`<Name of node_n_...>` é o nome de cada nó alocado para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="4aa62-201">`<Name of node_n_...>` is the name of each node allocated to this job.</span></span>
* <span data-ttu-id="4aa62-202">`<Cores of node_n_...>` é o número de núcleos no nó alocado para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="4aa62-202">`<Cores of node_n_...>` is the number of cores on the node allocated to this job.</span></span>

<span data-ttu-id="4aa62-203">O número de núcleos (**$NBCORES**) também é calculado com base no número de nós (**$NBNODES**) e no número de núcleos por nó (fornecido como o parâmetro **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="4aa62-203">The number of cores (**$NBCORES**) is also calculated based on the number of nodes (**$NBNODES**) and the number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="4aa62-204">Quanto às opções de MPI, as que são usadas com o Intel MPI no Azure são:</span><span class="sxs-lookup"><span data-stu-id="4aa62-204">For the MPI options, the ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="4aa62-205">`-mpi intel` para especificar o Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="4aa62-205">`-mpi intel` to specify Intel MPI.</span></span>
* <span data-ttu-id="4aa62-206">`-fabric UDAPL` para usar verbos do InfiniBand do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa62-206">`-fabric UDAPL` to use Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="4aa62-207">`-cpubind bandwidth,v` para otimizar a largura de banda para o MPI com o STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="4aa62-207">`-cpubind bandwidth,v` to optimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="4aa62-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` para fazer com que o Intel MPI funcione com o Azure InfiniBand e para definir o número necessário de núcleos por nó.</span><span class="sxs-lookup"><span data-stu-id="4aa62-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` to make Intel MPI work with Azure InfiniBand, and to set the required number of cores per node.</span></span>
* <span data-ttu-id="4aa62-209">`-batch` para iniciar o STAR-CCM+ no modo de lote sem nenhuma interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="4aa62-209">`-batch` to start STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="4aa62-210">Por fim, para iniciar um trabalho, certifique-se de que os nós estejam em funcionamento e estejam online no Gerenciador de Cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa62-210">Finally, to start a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="4aa62-211">Em seguida, de um prompt de comando do PowerShell execute:</span><span class="sxs-lookup"><span data-stu-id="4aa62-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="4aa62-212">Parar os nós</span><span class="sxs-lookup"><span data-stu-id="4aa62-212">Stop nodes</span></span>
<span data-ttu-id="4aa62-213">Posteriormente, depois de concluir seus testes, você pode usar os seguintes comandos do PowerShell do HPC Pack para parar e iniciar os nós:</span><span class="sxs-lookup"><span data-stu-id="4aa62-213">Later on, after you're done with your tests, you can use the following HPC Pack PowerShell commands to stop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="4aa62-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4aa62-214">Next steps</span></span>
<span data-ttu-id="4aa62-215">Tentar executar outras cargas de trabalho do Linux.</span><span class="sxs-lookup"><span data-stu-id="4aa62-215">Try running other Linux workloads.</span></span> <span data-ttu-id="4aa62-216">Por exemplo, consulte:</span><span class="sxs-lookup"><span data-stu-id="4aa62-216">For example, see:</span></span>

* [<span data-ttu-id="4aa62-217">Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="4aa62-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="4aa62-218">Executar o OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="4aa62-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
