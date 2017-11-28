---
title: aaaRun ESTRELA-CCM + com HPC Pack em VMs do Linux | Microsoft Docs
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
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="9486a-103">Executar o STAR-CCM+ com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="9486a-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="9486a-104">Este artigo mostra como toodeploy um Microsoft HPC Pack cluster no Azure e execute um [adapco CD ESTRELA-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) trabalho em vários nós de computação de Linux que estão interconectados com InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="9486a-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="9486a-105">Microsoft HPC Pack fornece recursos toorun uma variedade de HPC em larga escala e aplicativos em paralelo, incluindo aplicativos MPI, em clusters de máquinas virtuais do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9486a-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="9486a-106">O HPC Pack também dá suporte à execução de aplicativos de HPC do Linux em VMs com nós de computação do Linux implantadas em um cluster do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9486a-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="9486a-107">Para uma introdução toousing Linux nós com o HPC Pack de computação, consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9486a-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="9486a-108">Configurar um cluster do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="9486a-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="9486a-109">Fazer o download de scripts de implantação IaaS do HPC Pack Olá Olá [Centro de Download](https://www.microsoft.com/en-us/download/details.aspx?id=44949) e extraia-os localmente.</span><span class="sxs-lookup"><span data-stu-id="9486a-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="9486a-110">O Azure PowerShell é um pré-requisito.</span><span class="sxs-lookup"><span data-stu-id="9486a-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="9486a-111">Se o PowerShell não está configurado no seu computador local, leia o artigo da saudação [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9486a-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="9486a-112">Em tempo de saudação da redação deste artigo, imagens Linux Olá Olá Azure Marketplace (que contém os drivers de InfiniBand de saudação do Azure) são para 12 SLES, CentOS 6.5 e CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="9486a-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="9486a-113">Este artigo é com base no uso de saudação de 12 SLES.</span><span class="sxs-lookup"><span data-stu-id="9486a-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="9486a-114">nome de saudação tooretrieve de todas as imagens do Linux que dão suporte a HPC Olá Marketplace, você pode executar Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="9486a-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="9486a-115">saída de Hello lista local de saudação em que essas imagens estão disponíveis em Olá nome da imagem (**ImageName**) toobe usado no modelo de implantação de hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9486a-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="9486a-116">Antes de implantar o cluster hello, você tem toobuild um arquivo de modelo de implantação do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9486a-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="9486a-117">Porque estamos visando um pequeno cluster, o nó principal Olá Olá controlador de domínio e hospedar um banco de dados local do SQL.</span><span class="sxs-lookup"><span data-stu-id="9486a-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="9486a-118">Olá modelo a seguir será implantar tal um nó principal, crie um arquivo XML denominado **MyCluster.xml**e substitua os valores de saudação do **SubscriptionId**, **StorageAccount**,  **Local**, **VMName**, e **ServiceName** com as suas.</span><span class="sxs-lookup"><span data-stu-id="9486a-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

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

<span data-ttu-id="9486a-119">Inicie criação de nó de cabeçalho de saudação executando Olá comando do PowerShell em um prompt de comando elevado:</span><span class="sxs-lookup"><span data-stu-id="9486a-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="9486a-120">Depois de 20 minutos too30 nó principal Olá deve estar pronto.</span><span class="sxs-lookup"><span data-stu-id="9486a-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="9486a-121">Você pode se conectar tooit de saudação portal do Azure clicando Olá **conectar** ícone da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="9486a-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="9486a-122">Eventualmente, você pode ter o encaminhador de DNS Olá toofix.</span><span class="sxs-lookup"><span data-stu-id="9486a-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="9486a-123">toodo caso, inicie o Gerenciador de DNS.</span><span class="sxs-lookup"><span data-stu-id="9486a-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="9486a-124">Nome do servidor Olá com o botão direito no Gerenciador DNS, selecione **propriedades**e, em seguida, clique em Olá **encaminhadores** guia.</span><span class="sxs-lookup"><span data-stu-id="9486a-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="9486a-125">Clique em Olá **editar** botão tooremove os encaminhadores e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9486a-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="9486a-126">Certifique-se de que Olá **usar dicas de raiz, não se houver nenhuma encaminhadores** caixa de seleção está selecionada e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9486a-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="9486a-127">Configurar nós de computação do Linux</span><span class="sxs-lookup"><span data-stu-id="9486a-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="9486a-128">Implantar nós de computação Linux hello usando Olá mesmo modelo de implantação que você usou o nó principal do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="9486a-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="9486a-129">Copiar o arquivo de saudação **MyCluster.xml** no nó principal do computador local toohello e atualização Olá **NodeCount** marcar com número de saudação de nós que você deseja toodeploy (< = 20).</span><span class="sxs-lookup"><span data-stu-id="9486a-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="9486a-130">Ser cuidadoso toohave núcleos suficientes disponíveis em sua cota do Azure, porque cada instância A9 consumirá 16 núcleos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="9486a-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="9486a-131">Você pode usar instâncias A8 (8 núcleos) em vez de A9 se você quiser toouse mais VMs no hello mesmo orçamento.</span><span class="sxs-lookup"><span data-stu-id="9486a-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="9486a-132">No nó de cabeçalho hello, copie os scripts de implantação IaaS do HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="9486a-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="9486a-133">Olá executar comandos do PowerShell do Azure em um prompt de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9486a-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="9486a-134">Executar **Add-AzureAccount** tooconnect tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9486a-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="9486a-135">Se você tiver várias assinaturas, execute **Get-AzureSubscription** toolist-los.</span><span class="sxs-lookup"><span data-stu-id="9486a-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="9486a-136">Defina uma assinatura padrão executando Olá **Select-AzureSubscription - SubscriptionName xxxx-padrão** comando.</span><span class="sxs-lookup"><span data-stu-id="9486a-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="9486a-137">Executar **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart implantar nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="9486a-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![Implantação do nó principal em ação][hndeploy]

<span data-ttu-id="9486a-139">Abra a ferramenta de Gerenciador de Cluster do HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="9486a-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="9486a-140">Após alguns minutos, os nós de computação do Linux aparecerão regularmente na lista de nós de computação do cluster.</span><span class="sxs-lookup"><span data-stu-id="9486a-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="9486a-141">Com o modo de implantação clássico hello, as VMs de IaaS são criadas em sequência.</span><span class="sxs-lookup"><span data-stu-id="9486a-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="9486a-142">Então se o número de saudação de nós é importante, obter todos implantado pode levar uma quantidade significativa de tempo.</span><span class="sxs-lookup"><span data-stu-id="9486a-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Nós do Linux no Gerenciador de Cluster do HPC Pack][clustermanager]

<span data-ttu-id="9486a-144">Agora que todos os nós estão em execução no cluster hello, há toomake de configurações de infraestrutura adicional.</span><span class="sxs-lookup"><span data-stu-id="9486a-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="9486a-145">Configurar um compartilhamento de arquivos do Azure para nós do Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="9486a-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="9486a-146">Você pode usar scripts de toostore de serviços de arquivo do Azure hello, pacotes de aplicativos e arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="9486a-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="9486a-147">O arquivo do Azure fornece funcionalidades CIFS sobre o Armazenamento de Blobs do Azure como um repositório persistente.</span><span class="sxs-lookup"><span data-stu-id="9486a-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="9486a-148">Lembre-se de que isso não é solução mais dimensionável do hello, mas é Olá um mais simples e não requer VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="9486a-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="9486a-149">Criar um compartilhamento de arquivos do Azure seguindo as instruções de saudação artigo Olá [Introdução ao armazenamento de arquivo do Azure no Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="9486a-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="9486a-150">Manter Olá nome da sua conta de armazenamento como **saname**, nome de compartilhamento de arquivo hello como **sharename**e a chave de conta de armazenamento hello como **sakey**.</span><span class="sxs-lookup"><span data-stu-id="9486a-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="9486a-151">Compartilhamento de arquivo do Azure Olá montagem no nó de cabeçalho Olá</span><span class="sxs-lookup"><span data-stu-id="9486a-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="9486a-152">Abra um prompt de comando com privilégios elevados e execute Olá credenciais de saudação do comando toostore no cofre do computador local Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9486a-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="9486a-153">Em seguida, toomount hello Azure compartilhamento de arquivos, execute:</span><span class="sxs-lookup"><span data-stu-id="9486a-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="9486a-154">Montar o compartilhamento de arquivo do Azure Olá em nós de computação do Linux</span><span class="sxs-lookup"><span data-stu-id="9486a-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="9486a-155">Uma ferramenta útil que vem com o HPC Pack é a ferramenta de clusrun de saudação.</span><span class="sxs-lookup"><span data-stu-id="9486a-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="9486a-156">Você pode usar este Olá toorun de ferramenta de linha de comando mesmo comando simultaneamente em um conjunto de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="9486a-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="9486a-157">Em nosso caso, ele usou o compartilhamento de arquivo do Azure Olá toomount e mantê-lo toosurvive reinicializações.</span><span class="sxs-lookup"><span data-stu-id="9486a-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="9486a-158">Em um prompt de comando elevado no nó principal do hello, execute Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9486a-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="9486a-159">diretório de montagem Olá toocreate:</span><span class="sxs-lookup"><span data-stu-id="9486a-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="9486a-160">Olá toomount compartilhamento de arquivos do Azure:</span><span class="sxs-lookup"><span data-stu-id="9486a-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="9486a-161">compartilhamento de montagem de saudação toopersist:</span><span class="sxs-lookup"><span data-stu-id="9486a-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="9486a-162">Instalar o STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="9486a-162">Install STAR-CCM+</span></span>
<span data-ttu-id="9486a-163">As instâncias de VM do Azure A8 e A9 dão suporte ao InfiniBand e funcionalidades de RDMA.</span><span class="sxs-lookup"><span data-stu-id="9486a-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="9486a-164">drivers de kernel Olá habilitam esses recursos estão disponíveis para o Windows Server 2012 R2, SUSE 12, CentOS 6.5 e imagens CentOS 7.1 hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9486a-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="9486a-165">Microsoft MPI e Intel MPI (versão 5. x) são Olá duas MPI bibliotecas que dão suporte a esses drivers no Azure.</span><span class="sxs-lookup"><span data-stu-id="9486a-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="9486a-166">O STAR-CCM+ da CD-adapco versão 11.x e posterior é fornecido com o Intel MPI versão 5.x, portanto o suporte do InfiniBand para Azure está incluído.</span><span class="sxs-lookup"><span data-stu-id="9486a-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="9486a-167">Obter Olá Linux64 ESTRELA-CCM + pacote de saudação [CD adapco portal](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="9486a-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="9486a-168">Em nosso caso, usamos a versão 11.02.010 com precisão mista.</span><span class="sxs-lookup"><span data-stu-id="9486a-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="9486a-169">No nó de cabeçalho hello, em Olá **/hpcdata** arquivo do Azure compartilham, crie um script de shell chamado **setupstarccm.sh** com hello conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9486a-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="9486a-170">Esse script será executado em cada tooset do nó de computação backup ESTRELA-CCM + localmente.</span><span class="sxs-lookup"><span data-stu-id="9486a-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="9486a-171">Script setupstarcm.sh de exemplo</span><span class="sxs-lookup"><span data-stu-id="9486a-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="9486a-172">Agora, tooset backup ESTRELA-CCM + no seu Linux todos os nós de computação, abra um prompt de comando com privilégios elevados e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9486a-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="9486a-173">Enquanto estiver executando o comando hello, você pode monitorar o uso de CPU hello usando o mapa de calor de saudação do Gerenciador de Cluster.</span><span class="sxs-lookup"><span data-stu-id="9486a-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="9486a-174">Depois de alguns minutos, todos os nós devem estar instalados corretamente.</span><span class="sxs-lookup"><span data-stu-id="9486a-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="9486a-175">Executar trabalhos do STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="9486a-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="9486a-176">HPC Pack é usado para suas capacidades de Agendador de trabalho em ordem toorun ESTRELA-CCM + trabalhos.</span><span class="sxs-lookup"><span data-stu-id="9486a-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="9486a-177">toodo, portanto, é necessário Olá suporte de alguns scripts que são usados toostart trabalho de saudação e execute ESTRELA-CCM +.</span><span class="sxs-lookup"><span data-stu-id="9486a-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="9486a-178">dados de entrada Hello são mantidos em um compartilhamento de arquivo do Azure Olá primeiro para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="9486a-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="9486a-179">saudação de script do PowerShell a seguir é usado tooqueue uma ESTRELA-CCM + trabalho.</span><span class="sxs-lookup"><span data-stu-id="9486a-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="9486a-180">Ele usa três argumentos:</span><span class="sxs-lookup"><span data-stu-id="9486a-180">It takes three arguments:</span></span>

* <span data-ttu-id="9486a-181">nome do modelo Olá</span><span class="sxs-lookup"><span data-stu-id="9486a-181">hello model name</span></span>
* <span data-ttu-id="9486a-182">número de saudação de nós toobe usado</span><span class="sxs-lookup"><span data-stu-id="9486a-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="9486a-183">número de saudação de núcleos em cada toobe de nó usado</span><span class="sxs-lookup"><span data-stu-id="9486a-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="9486a-184">Porque ESTRELA-CCM + pode preencher largura de banda de memória Olá, é geralmente melhor toouse menos núcleos por nós de computação e adicionar novos nós.</span><span class="sxs-lookup"><span data-stu-id="9486a-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="9486a-185">número exato de saudação de núcleos por nó dependerá da família de processadores hello e velocidade de interconexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9486a-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="9486a-186">nós de saudação são alocados exclusivamente para trabalho hello e não podem ser compartilhadas com outros trabalhos.</span><span class="sxs-lookup"><span data-stu-id="9486a-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="9486a-187">trabalho de saudação não será iniciado como um trabalho MPI diretamente.</span><span class="sxs-lookup"><span data-stu-id="9486a-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="9486a-188">Olá **runstarccm.sh** script de shell iniciará o iniciador MPI hello.</span><span class="sxs-lookup"><span data-stu-id="9486a-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="9486a-189">saudação de entrada de modelo e Olá **runstarccm.sh** script são armazenados no hello **/hpcdata** compartilhamento anteriormente foi montado.</span><span class="sxs-lookup"><span data-stu-id="9486a-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="9486a-190">Arquivos de log são nomeados com a ID do trabalho hello e são armazenados no hello **/hpcdata compartilhamento**, juntamente com hello ESTRELA-CCM + arquivos de saída.</span><span class="sxs-lookup"><span data-stu-id="9486a-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="9486a-191">Script SubmitStarccmJob.ps1 de exemplo</span><span class="sxs-lookup"><span data-stu-id="9486a-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="9486a-192">Substitua **runner.java** por seu código de registro em log e código do iniciador de modelo Java do STAR-CCM+ preferidos.</span><span class="sxs-lookup"><span data-stu-id="9486a-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="9486a-193">Script runstarccm.sh de exemplo</span><span class="sxs-lookup"><span data-stu-id="9486a-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
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

<span data-ttu-id="9486a-194">Em nosso teste, usamos um token de licença do tipo Power-On-Demand.</span><span class="sxs-lookup"><span data-stu-id="9486a-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="9486a-195">Para esse token, você tem Olá tooset **$CDLMD_LICENSE_FILE** variável de ambiente muito **1999@flex.cd-adapco.com**  e chave Olá Olá **- podkey** opção de linha de comando Olá .</span><span class="sxs-lookup"><span data-stu-id="9486a-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="9486a-196">Após a inicialização de alguns, extrai script hello – de saudação **CCP_NODES_CORES $** variáveis de ambiente que defina HPC Pack - Olá lista de nós toobuild usa um arquivo de host que Olá iniciador MPI.</span><span class="sxs-lookup"><span data-stu-id="9486a-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="9486a-197">Esse arquivo de host vai conter uma lista de saudação dos nomes de nó de computação que são usados para trabalho hello, um nome por linha.</span><span class="sxs-lookup"><span data-stu-id="9486a-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="9486a-198">formato de saudação do **CCP_NODES_CORES $** segue este padrão:</span><span class="sxs-lookup"><span data-stu-id="9486a-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="9486a-199">Em que:</span><span class="sxs-lookup"><span data-stu-id="9486a-199">Where:</span></span>

* <span data-ttu-id="9486a-200">`<Number of nodes>`é o número de saudação de nós alocada toothis trabalho.</span><span class="sxs-lookup"><span data-stu-id="9486a-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="9486a-201">`<Name of node_n_...>`é o nome de saudação de cada nó alocada toothis trabalho.</span><span class="sxs-lookup"><span data-stu-id="9486a-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="9486a-202">`<Cores of node_n_...>`é o número de saudação de núcleos no nó Olá alocada toothis trabalho.</span><span class="sxs-lookup"><span data-stu-id="9486a-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="9486a-203">Olá número de núcleos (**$NBCORES**) também é calculada Olá com base no número de nós (**$NBNODES**) e o número de saudação de núcleos por nó (fornecido como parâmetro **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="9486a-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="9486a-204">Para obter opções de MPI hello, Olá aqueles que são usados com Intel MPI no Azure são:</span><span class="sxs-lookup"><span data-stu-id="9486a-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="9486a-205">`-mpi intel`toospecify Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9486a-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="9486a-206">`-fabric UDAPL`verbos toouse InfiniBand do Azure.</span><span class="sxs-lookup"><span data-stu-id="9486a-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="9486a-207">`-cpubind bandwidth,v`largura de banda toooptimize de MPI com ESTRELA-CCM +.</span><span class="sxs-lookup"><span data-stu-id="9486a-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="9486a-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI trabalhar com o Azure InfiniBand e tooset Olá obrigatório número de núcleos por nó.</span><span class="sxs-lookup"><span data-stu-id="9486a-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="9486a-209">`-batch`toostart ESTRELA-CCM + em modo de lote com nenhuma interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="9486a-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="9486a-210">Por fim, toostart um trabalho, certifique-se de que os nós estão funcionando e estão online no Gerenciador de Cluster.</span><span class="sxs-lookup"><span data-stu-id="9486a-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="9486a-211">Em seguida, de um prompt de comando do PowerShell execute:</span><span class="sxs-lookup"><span data-stu-id="9486a-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="9486a-212">Parar os nós</span><span class="sxs-lookup"><span data-stu-id="9486a-212">Stop nodes</span></span>
<span data-ttu-id="9486a-213">Posteriormente em, depois de concluir os testes, você pode usar o hello toostop de comandos do PowerShell do HPC Pack a seguir e iniciar os nós:</span><span class="sxs-lookup"><span data-stu-id="9486a-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="9486a-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9486a-214">Next steps</span></span>
<span data-ttu-id="9486a-215">Tentar executar outras cargas de trabalho do Linux.</span><span class="sxs-lookup"><span data-stu-id="9486a-215">Try running other Linux workloads.</span></span> <span data-ttu-id="9486a-216">Por exemplo, consulte:</span><span class="sxs-lookup"><span data-stu-id="9486a-216">For example, see:</span></span>

* [<span data-ttu-id="9486a-217">Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="9486a-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="9486a-218">Executar o OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="9486a-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
