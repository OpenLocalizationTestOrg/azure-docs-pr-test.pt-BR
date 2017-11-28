---
title: aaaSet um aplicativos de MPI Linux RDMA cluster toorun | Microsoft Docs
description: "Criar um cluster do Linux de toouse H16r, H16mr, A8 ou A9 VMs de tamanho Olá RDMA do Azure rede toorun MPI aplicativos"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="1ce69-103">Configurar um aplicativo de MPI toorun Linux RDMA cluster</span><span class="sxs-lookup"><span data-stu-id="1ce69-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="1ce69-104">Saiba como tooset a um RDMA Linux cluster no Azure com [tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun aplicativos de Interface MPI (Message Passing) paralelos.</span><span class="sxs-lookup"><span data-stu-id="1ce69-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="1ce69-105">Este artigo fornece etapas tooprepare um toorun de imagem do Linux HPC MPI Intel em um cluster.</span><span class="sxs-lookup"><span data-stu-id="1ce69-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="1ce69-106">Após a preparação, é possível implantar um cluster de VMs usando essa imagem e um dos tamanhos de máquina virtual do Azure compatíveis com RDMA hello (atualmente H16r, H16mr, A8 ou A9).</span><span class="sxs-lookup"><span data-stu-id="1ce69-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="1ce69-107">Use Olá cluster toorun MPI aplicativos que se comunicam com eficiência em uma rede de baixa latência, alta taxa de transferência com base na tecnologia de acesso (RDMA) de memória direta remota.</span><span class="sxs-lookup"><span data-stu-id="1ce69-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ce69-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e clássico.</span><span class="sxs-lookup"><span data-stu-id="1ce69-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="1ce69-109">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="1ce69-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="1ce69-110">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="1ce69-111">Opções de implantação de cluster</span><span class="sxs-lookup"><span data-stu-id="1ce69-111">Cluster deployment options</span></span>
<span data-ttu-id="1ce69-112">Estes são métodos que você pode usar toocreate um cluster Linux RDMA com ou sem um agendador de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1ce69-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="1ce69-113">**Scripts CLI do Azure**: conforme mostrado neste artigo, use Olá [interface de linha de comando do Azure](../../../cli-install-nodejs.md) implantação de saudação tooscript (CLI) de um cluster de VMs compatíveis com RDMA.</span><span class="sxs-lookup"><span data-stu-id="1ce69-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="1ce69-114">Olá CLI no modo de gerenciamento de serviço cria Olá nós de cluster em série no modelo de implantação clássico hello, para que implantar vários nós de computação pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="1ce69-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="1ce69-115">Olá tooenable conexão de rede RDMA quando você usa o modelo de implantação clássico hello, implantar VMs Olá no hello mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="1ce69-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="1ce69-116">**Modelos do Gerenciador de recursos do Azure**: você também pode usar toodeploy de modelo de implantação do hello Gerenciador de recursos um cluster de VMs compatíveis com RDMA que se conecta a rede RDMA toohello.</span><span class="sxs-lookup"><span data-stu-id="1ce69-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="1ce69-117">Você pode [criar seu próprio modelo](../../../resource-group-authoring-templates.md), ou verifique Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) para modelos de contribuição pela Microsoft ou hello comunidade toodeploy Olá solução desejada.</span><span class="sxs-lookup"><span data-stu-id="1ce69-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="1ce69-118">Modelos do Gerenciador de recursos podem fornecer uma maneira rápida e confiável toodeploy um cluster do Linux.</span><span class="sxs-lookup"><span data-stu-id="1ce69-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="1ce69-119">Olá tooenable conexão de rede RDMA quando você usa o modelo de implantação do Gerenciador de recursos de hello, implantar VMs de saudação em Olá mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="1ce69-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="1ce69-120">**HPC Pack**: criar um cluster do Microsoft HPC Pack no Azure e adicionar nós de computação compatíveis com RDMA que executam uma rede com suporte Linux distribuição tooaccess Olá RDMA.</span><span class="sxs-lookup"><span data-stu-id="1ce69-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="1ce69-121">Para saber mais, confira [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1ce69-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="1ce69-122">As etapas de implantação de exemplo no modelo clássico Olá</span><span class="sxs-lookup"><span data-stu-id="1ce69-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="1ce69-123">Olá etapas a seguir mostram como toouse Olá CLI do Azure toodeploy uma VM do SUSE Linux Enterprise Server (SLES) 12 SP1 HPC de saudação do Azure Marketplace, personalizá-lo e criar uma imagem VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="1ce69-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="1ce69-124">Em seguida, você pode usar implantação da saudação tooscript Olá imagem de um cluster de VMs compatíveis com RDMA.</span><span class="sxs-lookup"><span data-stu-id="1ce69-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="1ce69-125">Use semelhante toodeploy etapas que um cluster de VMs compatíveis com RDMA baseado nas imagens com base em CentOS HPC hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1ce69-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="1ce69-126">Algumas etapas são ligeiramente diferentes, conforme observado.</span><span class="sxs-lookup"><span data-stu-id="1ce69-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="1ce69-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1ce69-127">Prerequisites</span></span>
* <span data-ttu-id="1ce69-128">**Computador cliente**: É necessário um toocommunicate de computador cliente Mac, Linux ou Windows com o Azure.</span><span class="sxs-lookup"><span data-stu-id="1ce69-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="1ce69-129">Essas etapas pressupõem que você esteja usando um cliente Linux.</span><span class="sxs-lookup"><span data-stu-id="1ce69-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="1ce69-130">**Assinatura do Azure**: se não tiver uma assinatura, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="1ce69-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="1ce69-131">Para clusters maiores, considere uma assinatura pré-paga ou outras opções de compra.</span><span class="sxs-lookup"><span data-stu-id="1ce69-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="1ce69-132">**Disponibilidade de tamanho VM**: Olá tamanhos de instância a seguir é capazes de RDMA: H16r, H16mr, A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="1ce69-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="1ce69-133">Confira [Produtos disponíveis por região](https://azure.microsoft.com/regions/services/) para ver a disponibilidade nas regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ce69-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="1ce69-134">**Cota de núcleos**: você pode precisar de uma cota de saudação tooincrease de núcleos toodeploy um cluster de computação intensa VMs.</span><span class="sxs-lookup"><span data-stu-id="1ce69-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="1ce69-135">Por exemplo, você precisa, pelo menos, 128 núcleos, se você deseja toodeploy 8 A9 VMs conforme mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="1ce69-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="1ce69-136">Sua assinatura também pode limitar o número de saudação de núcleos que podem ser implantados em determinadas famílias de tamanho VM, incluindo Olá H-series.</span><span class="sxs-lookup"><span data-stu-id="1ce69-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="1ce69-137">aumentar a cota toorequest, [abrir uma solicitação de suporte do cliente online](../../../azure-supportability/how-to-create-azure-support-request.md) sem custo adicional.</span><span class="sxs-lookup"><span data-stu-id="1ce69-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="1ce69-138">**CLI do Azure**: [instalar](../../../cli-install-nodejs.md) Olá CLI do Azure e [conectar tooyour assinatura do Azure](../../../xplat-cli-connect.md) do computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="1ce69-139">Provisionar uma VM do HPC para SLES 12 SP1</span><span class="sxs-lookup"><span data-stu-id="1ce69-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="1ce69-140">Depois de entrar no tooAzure com hello CLI do Azure, execute `azure config list` tooconfirm que Olá a saída mostra o modo de gerenciamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1ce69-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="1ce69-141">Se não estiver, defina o modo de saudação executando este comando:</span><span class="sxs-lookup"><span data-stu-id="1ce69-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="1ce69-142">Digite hello toolist a seguir todas as assinaturas de saudação são toouse autorizado:</span><span class="sxs-lookup"><span data-stu-id="1ce69-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="1ce69-143">assinatura ativa atual de saudação é identificada com `Current` definido muito`true`.</span><span class="sxs-lookup"><span data-stu-id="1ce69-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="1ce69-144">Se esta assinatura não for Olá você deseja toouse toocreate Olá cluster, defina ID de assinatura apropriada Olá como assinatura ativa hello:</span><span class="sxs-lookup"><span data-stu-id="1ce69-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="1ce69-145">toosee Olá disponíveis publicamente imagens SLES 12 SP1 HPC no Azure, execute um comando como Olá a seguir, supondo que seu ambiente de shell oferece suporte à **grep**:</span><span class="sxs-lookup"><span data-stu-id="1ce69-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="1ce69-146">Provisione uma VM compatíveis com RDMA com uma imagem de HPC de SP1 12 SLES executando um comando como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ce69-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="1ce69-147">Em que:</span><span class="sxs-lookup"><span data-stu-id="1ce69-147">Where:</span></span>

* <span data-ttu-id="1ce69-148">Olá tamanho (A9 neste exemplo) é um dos tamanhos de VM Olá compatíveis com RDMA.</span><span class="sxs-lookup"><span data-stu-id="1ce69-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="1ce69-149">Olá externo número da porta SSH (22 neste exemplo, o que é o saudação padrão SSH) é qualquer número de porta válido.</span><span class="sxs-lookup"><span data-stu-id="1ce69-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="1ce69-150">número da porta SSH interno Olá é definido too22.</span><span class="sxs-lookup"><span data-stu-id="1ce69-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="1ce69-151">Um novo serviço de nuvem é criado no hello região do Azure especificada pelo Olá local.</span><span class="sxs-lookup"><span data-stu-id="1ce69-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="1ce69-152">Especifique um local no qual Olá VM tamanho escolhido está disponível.</span><span class="sxs-lookup"><span data-stu-id="1ce69-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="1ce69-153">Para suporte de prioridade SUSE (que implica em custo adicional), nome da imagem Olá SP1 de 12 SLES atualmente pode ser uma destas duas opções:</span><span class="sxs-lookup"><span data-stu-id="1ce69-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="1ce69-154">Personalizar Olá VM</span><span class="sxs-lookup"><span data-stu-id="1ce69-154">Customize hello VM</span></span>
<span data-ttu-id="1ce69-155">Após a conclusão da saudação VM provisionamento, SSH toohello VM usando Olá endereço IP externo da VM (ou nome DNS) e Olá número da porta externa configurado e, em seguida, personalizá-lo.</span><span class="sxs-lookup"><span data-stu-id="1ce69-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="1ce69-156">Para obter detalhes de conexão, consulte [como toolog na máquina virtual de tooa executando o Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ce69-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1ce69-157">Execute comandos como usuário Olá configurado no hello VM, a menos que o acesso à raiz é necessário toocomplete uma etapa.</span><span class="sxs-lookup"><span data-stu-id="1ce69-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ce69-158">Microsoft Azure não fornece acesso à raiz tooLinux VMs.</span><span class="sxs-lookup"><span data-stu-id="1ce69-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="1ce69-159">acesso administrativo de toogain quando conectado como um usuário toohello VM, execute comandos usando `sudo`.</span><span class="sxs-lookup"><span data-stu-id="1ce69-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="1ce69-160">**Atualizações**: instale atualizações usando o zypper.</span><span class="sxs-lookup"><span data-stu-id="1ce69-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="1ce69-161">Você também poderá tooinstall utilitários NFS.</span><span class="sxs-lookup"><span data-stu-id="1ce69-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1ce69-162">Em uma VM de HPC SLES 12 SP1, é recomendável que você não aplicar as atualizações de kernel, que podem causar problemas com hello Linux RDMA drivers.</span><span class="sxs-lookup"><span data-stu-id="1ce69-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="1ce69-163">**Intel MPI**: Concluir instalação de saudação do Intel MPI no hello SLES 12 SP1 HPC VM executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ce69-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="1ce69-164">**Bloquear memória**: MPI códigos toolock Olá memória disponível para o RDMA, adicionar ou alterar Olá configurações no arquivo de /etc/security/limits.conf Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="1ce69-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="1ce69-165">Você precisa raiz acesso tooedit esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="1ce69-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="1ce69-166">Para fins de teste, você também pode definir memlock toounlimited.</span><span class="sxs-lookup"><span data-stu-id="1ce69-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="1ce69-167">Por exemplo: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="1ce69-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="1ce69-168">Para saber mais, confira [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size) (Métodos mais conhecidos para definir o tamanho da memória bloqueada).</span><span class="sxs-lookup"><span data-stu-id="1ce69-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="1ce69-169">**As chaves de SSH para VMs SLES**: gerar SSH chaves tooestablish confiança para sua conta de usuário entre Olá nós de computação no cluster do SLES hello quando executar trabalhos MPI.</span><span class="sxs-lookup"><span data-stu-id="1ce69-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="1ce69-170">Se você tiver implantado uma VM do HPC baseado em CentOS, não execute esta etapa.</span><span class="sxs-lookup"><span data-stu-id="1ce69-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="1ce69-171">Consulte as instruções posteriormente tooset este artigo a relação de confiança SSH passwordless entre nós de cluster Olá depois de capturar a imagem de saudação e implantar um cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="1ce69-172">chaves SSH toocreate, executadas Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="1ce69-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="1ce69-173">Quando você for solicitado para a entrada, selecione **Enter** toogenerate chaves de saudação no local padrão de saudação sem definir uma senha.</span><span class="sxs-lookup"><span data-stu-id="1ce69-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="1ce69-174">Anexar o arquivo de authorized_keys Olá toohello de chave pública para chaves públicas conhecidas.</span><span class="sxs-lookup"><span data-stu-id="1ce69-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="1ce69-175">No diretório de ~/.ssh hello, editar ou criar o arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="1ce69-176">Forneça o intervalo de endereços IP hello de rede privada Olá que você planeje toouse no Azure (10.32.0.0/16 neste exemplo):</span><span class="sxs-lookup"><span data-stu-id="1ce69-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="1ce69-177">Como alternativa, lista o endereço IP de rede privada de saudação de cada VM no seu cluster da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1ce69-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="1ce69-178">A configuração de `StrictHostKeyChecking no` pode criar um risco de segurança potencial quando um determinado endereço IP ou intervalo não for especificado.</span><span class="sxs-lookup"><span data-stu-id="1ce69-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="1ce69-179">**Aplicativos**: instalar os aplicativos necessários ou executar outras personalizações antes de capturar a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="1ce69-180">Capturar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="1ce69-180">Capture hello image</span></span>
<span data-ttu-id="1ce69-181">imagem toocapture hello, primeiro execute Olá comando a seguir no hello VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="1ce69-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="1ce69-182">Esse comando deprovisions Olá VM, mas mantém a contas de usuário e as chaves de SSH que você configurou.</span><span class="sxs-lookup"><span data-stu-id="1ce69-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="1ce69-183">No computador cliente, execute Olá após a imagem de saudação do toocapture de comandos de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ce69-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="1ce69-184">Para obter mais informações, consulte [como uma máquina de virtual do Linux clássica como uma imagem de toocapture](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="1ce69-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="1ce69-185">Depois de executar esses comandos, a imagem da VM Olá é capturada para seu uso e Olá VM é excluído.</span><span class="sxs-lookup"><span data-stu-id="1ce69-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="1ce69-186">Agora você tem o toodeploy pronto de imagem personalizada um cluster.</span><span class="sxs-lookup"><span data-stu-id="1ce69-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="1ce69-187">Implantar um cluster com a imagem de saudação</span><span class="sxs-lookup"><span data-stu-id="1ce69-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="1ce69-188">Modificar Olá Bash script com valores apropriados para o seu ambiente a seguir e executá-lo do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="1ce69-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="1ce69-189">Porque o Azure implanta VMs Olá em série no modelo de implantação clássico hello, ele leva alguns minutos toodeploy Olá oito VMs A9 sugerido neste script.</span><span class="sxs-lookup"><span data-stu-id="1ce69-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="1ce69-190">Considerações para um cluster de HPC do CentOS</span><span class="sxs-lookup"><span data-stu-id="1ce69-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="1ce69-191">Se você quiser tooset um cluster com base em uma das imagens HPC com base em CentOS Olá no hello Azure Marketplace em vez de 12 SLES para HPC, siga etapas gerais Olá Olá anterior da seção.</span><span class="sxs-lookup"><span data-stu-id="1ce69-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="1ce69-192">Observe Olá diferenças a seguir quando você provisionar e configurar Olá VM:</span><span class="sxs-lookup"><span data-stu-id="1ce69-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="1ce69-193">O Intel MPI já está instalado em uma VM provisionada de uma imagem do HPC baseado em CentOS.</span><span class="sxs-lookup"><span data-stu-id="1ce69-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="1ce69-194">Configurações de memória de bloqueio já foram adicionadas no arquivo de /etc/security/limits.conf de saudação da VM.</span><span class="sxs-lookup"><span data-stu-id="1ce69-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="1ce69-195">Não gere chaves SSH no hello VM provisionar para captura.</span><span class="sxs-lookup"><span data-stu-id="1ce69-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="1ce69-196">Em vez disso, é recomendável configurar a autenticação baseada em usuário após a implantação de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="1ce69-197">Para obter mais informações, consulte Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="1ce69-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="1ce69-198">Configurar confiança passwordless do SSH no cluster Olá</span><span class="sxs-lookup"><span data-stu-id="1ce69-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="1ce69-199">Em um cluster HPC com base em CentOS, há dois métodos para estabelecer confiança entre nós de computação Olá: autenticação baseada em host e a autenticação baseada em usuário.</span><span class="sxs-lookup"><span data-stu-id="1ce69-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="1ce69-200">Autenticação baseada em host está fora do escopo deste artigo hello e geralmente deve ser feita por meio de um script de extensão durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="1ce69-201">Autenticação baseada em usuário é conveniente para estabelecer confiança após a implantação e requer o compartilhamento de chaves SSH entre hello e geração de saudação nós de computação em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1ce69-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="1ce69-202">Esse método é conhecido como logon SSH sem senha e é necessário na execução de trabalhos MPI.</span><span class="sxs-lookup"><span data-stu-id="1ce69-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="1ce69-203">Está disponível em um script de exemplo a contribuição da comunidade Olá [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) autenticação de usuário fácil tooenable em um cluster HPC com base em CentOS.</span><span class="sxs-lookup"><span data-stu-id="1ce69-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="1ce69-204">Baixar e usar esse script usando Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="1ce69-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="1ce69-205">Você também pode modificar o script ou usar qualquer outra método tooestablish passwordless autenticação SSH entre nós de computação de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1ce69-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="1ce69-206">script de saudação toorun, é necessário tooknow prefixo de saudação para seus endereços IP de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="1ce69-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="1ce69-207">Obtenha o prefixo Olá executando Olá comando a seguir em um de nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="1ce69-208">A saída deve ser algo como 10.1.3.5 e prefixo Olá é parte de saudação 10.1.3.</span><span class="sxs-lookup"><span data-stu-id="1ce69-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="1ce69-209">Agora execute o script hello usando três parâmetros: nome de usuário comuns Olá no hello nós de computação, senha comum Olá para nós de computação do usuário em hello e prefixo de sub-rede Olá que foi retornada do comando anterior hello.</span><span class="sxs-lookup"><span data-stu-id="1ce69-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="1ce69-210">Esse script hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ce69-210">This script does hello following:</span></span>

* <span data-ttu-id="1ce69-211">Cria um diretório no nó de host Olá denominado .ssh, que é necessário para logon passwordless.</span><span class="sxs-lookup"><span data-stu-id="1ce69-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="1ce69-212">Cria um arquivo de configuração no diretório de .ssh Olá que instrui o logon de tooallow passwordless logon de qualquer nó no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="1ce69-213">Cria arquivos que contêm nomes de nó hello e endereços IP do nó de todos os nós de saudação em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1ce69-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="1ce69-214">Esses arquivos são deixados após a execução de script hello para referência posterior.</span><span class="sxs-lookup"><span data-stu-id="1ce69-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="1ce69-215">Cria um par de chaves público e privado para cada nó de cluster (incluindo o nó do host Olá) e cria entradas no arquivo de authorized_keys hello.</span><span class="sxs-lookup"><span data-stu-id="1ce69-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="1ce69-216">A execução desse script pode criar um potencial risco de segurança.</span><span class="sxs-lookup"><span data-stu-id="1ce69-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="1ce69-217">Certifique-se de que as informações de chave pública do hello em ~/.ssh não são distribuídas.</span><span class="sxs-lookup"><span data-stu-id="1ce69-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="1ce69-218">Configurar o Intel MPI</span><span class="sxs-lookup"><span data-stu-id="1ce69-218">Configure Intel MPI</span></span>
<span data-ttu-id="1ce69-219">aplicativos de MPI toorun em RDMA de Linux do Azure, você precisa tooconfigure determinado tooIntel da específico de variáveis de ambiente MPI.</span><span class="sxs-lookup"><span data-stu-id="1ce69-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="1ce69-220">Aqui está um exemplo Bash script tooconfigure Olá variáveis necessárias toorun um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ce69-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="1ce69-221">Altere Olá caminho toompivars.sh conforme necessário para a instalação do Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="1ce69-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="1ce69-222">formato de Olá Olá do arquivo do host é o seguinte.</span><span class="sxs-lookup"><span data-stu-id="1ce69-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="1ce69-223">Adicione uma linha para cada nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="1ce69-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="1ce69-224">Especifique os endereços IP privados da rede virtual Olá definido anteriormente, não os nomes DNS.</span><span class="sxs-lookup"><span data-stu-id="1ce69-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="1ce69-225">Por exemplo, para dois hosts com endereços IP 10.32.0.1 e 10.32.0.2, o arquivo hello contém seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="1ce69-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="1ce69-226">Executar MPI em um cluster de dois nós básico</span><span class="sxs-lookup"><span data-stu-id="1ce69-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="1ce69-227">Se você ainda não fez isso, primeiro defina o ambiente de saudação para Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="1ce69-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="1ce69-228">Executar um comando MPI</span><span class="sxs-lookup"><span data-stu-id="1ce69-228">Run an MPI command</span></span>
<span data-ttu-id="1ce69-229">Execute um comando MPI em uma saudação tooshow de nós de computação que MPI está instalado corretamente e pode se comunicar entre pelo menos dois nós de computação.</span><span class="sxs-lookup"><span data-stu-id="1ce69-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="1ce69-230">a seguir Olá **mpirun** comando executa Olá **hostname** comando em dois nós.</span><span class="sxs-lookup"><span data-stu-id="1ce69-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="1ce69-231">A saída deve listar os nomes de saudação de todos os nós de saudação passado como entrada para `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="1ce69-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="1ce69-232">Por exemplo, um **mpirun** comando com dois nós retorna a saída como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="1ce69-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="1ce69-233">Executar um parâmetro de comparação de MPI</span><span class="sxs-lookup"><span data-stu-id="1ce69-233">Run an MPI benchmark</span></span>
<span data-ttu-id="1ce69-234">Olá Intel MPI comando a seguir executa uma pingpong benchmark tooverify Olá configuração e conexão toohello RDMA rede de cluster.</span><span class="sxs-lookup"><span data-stu-id="1ce69-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="1ce69-235">Em um cluster com dois nós de trabalho, você deve ver a saída como Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="1ce69-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="1ce69-236">Na rede de RDMA do Azure Olá, espere latência ou abaixo 3 microssegundos de tamanhos de mensagem too512 bytes.</span><span class="sxs-lookup"><span data-stu-id="1ce69-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="1ce69-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ce69-237">Next steps</span></span>
* <span data-ttu-id="1ce69-238">Implantar e executar os aplicativos MPI do Linux no cluster do Linux.</span><span class="sxs-lookup"><span data-stu-id="1ce69-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="1ce69-239">Consulte Olá [documentação da Intel MPI biblioteca](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) para obter orientação sobre Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="1ce69-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="1ce69-240">Tente uma [quickstart modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate um Lustre Intel cluster usando uma imagem com base em CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="1ce69-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="1ce69-241">Para obter detalhes, confira [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/) (Implantando o Intel Cloud Edition for Lustre no Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="1ce69-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
