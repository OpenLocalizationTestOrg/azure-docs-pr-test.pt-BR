---
title: Clusterizar MySQL com conjuntos com balanceamento de carga | Microsoft Docs
description: "Configurar um cluster MySQL do Linux com alta disponibilidade e balanceamento de carga criado com o modelo clássico de implantação no Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 4eaf86c9ac3e4dc2b51b88383626eda774cab0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-load-balanced-sets-to-clusterize-mysql-on-linux"></a><span data-ttu-id="24548-103">Use os conjuntos de carga balanceada para clusterizar MySQL no Linux</span><span class="sxs-lookup"><span data-stu-id="24548-103">Use load-balanced sets to clusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="24548-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e Clássico.</span><span class="sxs-lookup"><span data-stu-id="24548-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="24548-105">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="24548-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="24548-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="24548-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="24548-107">Um [modelo do Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) estará disponível se você precisar implantar um cluster do MySQL.</span><span class="sxs-lookup"><span data-stu-id="24548-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span></span>

<span data-ttu-id="24548-108">Este artigo explora e ilustra as diferentes abordagens disponíveis para implantar serviços com base em Linux, altamente disponíveis no Microsoft Azure, explorando a alta disponibilidade do MySQL Server como elemento principal.</span><span class="sxs-lookup"><span data-stu-id="24548-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="24548-109">Há um vídeo ilustrando essa abordagem disponível no [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="24548-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="24548-110">Descrevemos uma solução de alta disponibilidade do MySQL de mestre único, dois nós e sem compartilhar nada, com base em DRBD, Corosync e Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="24548-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="24548-111">Apenas um nó executa o MySQL por vez.</span><span class="sxs-lookup"><span data-stu-id="24548-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="24548-112">A leitura e a gravação do recurso DRBD também está limitada a apenas um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="24548-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span></span>

<span data-ttu-id="24548-113">Não há necessidade de uma solução VIP como LVS porque você usará os conjuntos de balanceamento de carga no Microsoft Azure para fornecer a funcionalidade de round robin e detecção do ponto de extremidade, além da remoção e recuperação normal do VIP.</span><span class="sxs-lookup"><span data-stu-id="24548-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span></span> <span data-ttu-id="24548-114">O VIP é um endereço IPv4 roteável globalmente, atribuído pelo Microsoft Azure ao criarmos o serviço de nuvem pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="24548-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span></span>

<span data-ttu-id="24548-115">Existem outras arquiteturas possíveis para MySQL, inclusive NBD Cluster, Percona e Galera, bem como diversas soluções de middleware, incluindo pelo menos uma disponível como uma VM no [Repositório de VM](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="24548-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="24548-116">Como essas soluções podem replicar em unicast X multicast ou difusão e não dependem de armazenamento compartilhado ou de várias interfaces de rede, os cenários devem ser fáceis de implantar no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="24548-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span></span>

<span data-ttu-id="24548-117">Essas arquiteturas de clustering podem ser estendidas até outro produtos como PostgreSQL e OpenLDAP de maneira semelhante.</span><span class="sxs-lookup"><span data-stu-id="24548-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="24548-118">Por exemplo, esse procedimento de balanceamento de carga sem compartilhar nada foi testado com êxito com o OpenLDAP multimestres e é possível ver isso em nosso blog Channel 9.</span><span class="sxs-lookup"><span data-stu-id="24548-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="24548-119">Prepare-se</span><span class="sxs-lookup"><span data-stu-id="24548-119">Get ready</span></span>
<span data-ttu-id="24548-120">É necessário ter os seguintes recursos e capacidades:</span><span class="sxs-lookup"><span data-stu-id="24548-120">You need the following resources and abilities:</span></span>

  - <span data-ttu-id="24548-121">Uma conta do Microsoft Azure com uma assinatura válida, capaz de criar pelo menos duas VMs (XS foi usado neste exemplo)</span><span class="sxs-lookup"><span data-stu-id="24548-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="24548-122">Uma rede e uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="24548-122">A network and a subnet</span></span>
  - <span data-ttu-id="24548-123">Um grupo de afinidades</span><span class="sxs-lookup"><span data-stu-id="24548-123">An affinity group</span></span>
  - <span data-ttu-id="24548-124">Um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="24548-124">An availability set</span></span>
  - <span data-ttu-id="24548-125">A capacidade de criar VHDs na mesma região que o serviço de nuvem e anexá-los às VMs Linux</span><span class="sxs-lookup"><span data-stu-id="24548-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="24548-126">Ambiente testado</span><span class="sxs-lookup"><span data-stu-id="24548-126">Tested environment</span></span>
* <span data-ttu-id="24548-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="24548-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="24548-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="24548-128">DRBD</span></span>
  * <span data-ttu-id="24548-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="24548-129">MySQL Server</span></span>
  * <span data-ttu-id="24548-130">Corosync e Pacemaker</span><span class="sxs-lookup"><span data-stu-id="24548-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="24548-131">Grupo de afinidade</span><span class="sxs-lookup"><span data-stu-id="24548-131">Affinity group</span></span>
<span data-ttu-id="24548-132">Crie um grupo de afinidades para a solução de entrando no Portal Clássico do Azure, selecionando **Configurações** e criando um novo grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="24548-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="24548-133">Os recursos alocados criados posteriormente serão atribuídos a esse grupo de afinidade.</span><span class="sxs-lookup"><span data-stu-id="24548-133">Allocated resources created later will be assigned to this affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="24548-134">Redes</span><span class="sxs-lookup"><span data-stu-id="24548-134">Networks</span></span>
<span data-ttu-id="24548-135">Uma nova rede é criada, e uma sub-rede é criada dentro da rede.</span><span class="sxs-lookup"><span data-stu-id="24548-135">A new network is created, and a subnet is created inside the network.</span></span> <span data-ttu-id="24548-136">Este exemplo usa uma rede 10.10.10.0/24 com apenas uma sub-rede /24 interna.</span><span class="sxs-lookup"><span data-stu-id="24548-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="24548-137">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="24548-137">Virtual machines</span></span>
<span data-ttu-id="24548-138">A primeira VM do Ubuntu 13.10 é criada usando-se uma imagem da Endorsed Ubuntu Gallery, chamada `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="24548-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="24548-139">Um novo serviço de nuvem é criado no processo, chamado hadb.</span><span class="sxs-lookup"><span data-stu-id="24548-139">A new cloud service is created in the process, called hadb.</span></span> <span data-ttu-id="24548-140">Esse nome para ilustrar a natureza compartilhada e de balanceamento de carga que o serviço terá quando adicionarmos mais recursos.</span><span class="sxs-lookup"><span data-stu-id="24548-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span></span> <span data-ttu-id="24548-141">A criação de `hadb01` ocorre sem erros e é concluída usando o portal.</span><span class="sxs-lookup"><span data-stu-id="24548-141">The creation of `hadb01` is uneventful and completed by using the portal.</span></span> <span data-ttu-id="24548-142">Um ponto de extremidade para SSH é criado automaticamente e a nova rede criada é selecionada.</span><span class="sxs-lookup"><span data-stu-id="24548-142">An endpoint for SSH is automatically created, and the new network is selected.</span></span> <span data-ttu-id="24548-143">Agora você pode criar um conjunto de disponibilidade para as VMs.</span><span class="sxs-lookup"><span data-stu-id="24548-143">Now you can create an availability set for the VMs.</span></span>

<span data-ttu-id="24548-144">Depois que a primeira VM for criada (tecnicamente, quando o serviço de nuvem é criado), crie a segunda VM, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="24548-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span></span> <span data-ttu-id="24548-145">Para a segunda VM, usaremos a VM do Ubuntu 13.10 na Galeria usando o portal, porém use um serviço de nuvem existente, `hadb.cloudapp.net`, em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="24548-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="24548-146">A rede e o conjunto de disponibilidade deverão ser selecionados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="24548-146">The network and availability set should be automatically selected.</span></span> <span data-ttu-id="24548-147">Também será criado um ponto de extremidade SSH.</span><span class="sxs-lookup"><span data-stu-id="24548-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="24548-148">Depois que ambas as VMs forem criadas, anotaremos a porta SSH de `hadb01` (TCP 22) e de `hadb02` (atribuída automaticamente pelo Azure).</span><span class="sxs-lookup"><span data-stu-id="24548-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="24548-149">Armazenamento anexado</span><span class="sxs-lookup"><span data-stu-id="24548-149">Attached storage</span></span>
<span data-ttu-id="24548-150">Anexe um novo disco a ambas as VMs e crie discos de 5 GB no processo.</span><span class="sxs-lookup"><span data-stu-id="24548-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span></span> <span data-ttu-id="24548-151">Os discos serão hospedados no contêiner VHD em uso para os discos do sistema operacional principal.</span><span class="sxs-lookup"><span data-stu-id="24548-151">The disks are hosted in the VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="24548-152">Depois que os discos forem criados e anexados não há necessidade de reiniciar o Linux, pois o kernel verá o novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24548-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span></span> <span data-ttu-id="24548-153">Este dispositivo é normalmente `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="24548-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="24548-154">Verifique `dmesg` para ver a saída.</span><span class="sxs-lookup"><span data-stu-id="24548-154">Check `dmesg` for the output.</span></span>

<span data-ttu-id="24548-155">Em cada VM, crie uma partição usando `cfdisk` (primária, partição do Linux) e grave a nova tabela de partição.</span><span class="sxs-lookup"><span data-stu-id="24548-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span></span> <span data-ttu-id="24548-156">Não crie um sistema de arquivos nessa partição.</span><span class="sxs-lookup"><span data-stu-id="24548-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-the-cluster"></a><span data-ttu-id="24548-157">Configurar o cluster</span><span class="sxs-lookup"><span data-stu-id="24548-157">Set up the cluster</span></span>
<span data-ttu-id="24548-158">Use o APT para instalar Corosync, Pacemaker e DRBD em ambas as VMs Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="24548-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="24548-159">Para fazer isso com `apt-get`, execute o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="24548-159">To do so with `apt-get`, run the following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="24548-160">Não instale o MySQL neste momento.</span><span class="sxs-lookup"><span data-stu-id="24548-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="24548-161">Os scripts de instalação do Debian e do Ubuntu inicializarão um diretório de dados do MySQL em `/var/lib/mysql`, mas como o diretório será substituído por um sistema de arquivos DRBD, será necessário instalar o MySQL mais tarde.</span><span class="sxs-lookup"><span data-stu-id="24548-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span></span>

<span data-ttu-id="24548-162">Verifique (usando `/sbin/ifconfig`) se ambas as VMs estão usando endereços na sub-rede 10.10.10.0/24 e se podem executar ping uma na outra pelo nome.</span><span class="sxs-lookup"><span data-stu-id="24548-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="24548-163">Você também pode usar `ssh-keygen` e `ssh-copy-id` para verificar se ambas as VMs conseguem se comunicar via SSH sem exigir uma senha.</span><span class="sxs-lookup"><span data-stu-id="24548-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="24548-164">Configurar DRBD</span><span class="sxs-lookup"><span data-stu-id="24548-164">Set up DRBD</span></span>
<span data-ttu-id="24548-165">Crie um recurso DRBD que usa a partição subjacente `/dev/sdc1` para produzir um recurso `/dev/drbd1` capaz de ser formatado usando ext3 e usado em nós primários e secundários.</span><span class="sxs-lookup"><span data-stu-id="24548-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="24548-166">Abra `/etc/drbd.d/r0.res` e copie a definição de recurso a seguir em ambas as VMs:</span><span class="sxs-lookup"><span data-stu-id="24548-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="24548-167">Inicialize o recurso usando `drbdadm` em ambas as VMs:</span><span class="sxs-lookup"><span data-stu-id="24548-167">Initialize the resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="24548-168">Na VM primária (`hadb01`), force a propriedade (primária) do recurso DRBD:</span><span class="sxs-lookup"><span data-stu-id="24548-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="24548-169">Se examinar o conteúdo de /proc/drbd (`sudo cat /proc/drbd`) em ambas as VMs, você deve ver `Primary/Secondary` em `hadb01` e `Secondary/Primary` em `hadb02`, consistente com a solução até o momento.</span><span class="sxs-lookup"><span data-stu-id="24548-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span></span> <span data-ttu-id="24548-170">O disco de 5 GB será sincronizado na rede 10.10.10.0/24 sem encargos para os clientes.</span><span class="sxs-lookup"><span data-stu-id="24548-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span></span>

<span data-ttu-id="24548-171">Assim que o disco for sincronizado, será possível criar o sistema de arquivos em `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="24548-171">After the disk is synchronized, you can create the file system on `hadb01`.</span></span> <span data-ttu-id="24548-172">Usamos ext2 para fins de testes, mas a seguinte instrução criará um sistema de arquivos ext3:</span><span class="sxs-lookup"><span data-stu-id="24548-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-the-drbd-resource"></a><span data-ttu-id="24548-173">Montando o recurso DRBD</span><span class="sxs-lookup"><span data-stu-id="24548-173">Mount the DRBD resource</span></span>
<span data-ttu-id="24548-174">Agora você está pronto para montar os recursos DRBD no `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="24548-174">You're now ready to mount the DRBD resources on `hadb01`.</span></span> <span data-ttu-id="24548-175">Debian e derivativos usam `/var/lib/mysql` como diretório de dados do MySQL.</span><span class="sxs-lookup"><span data-stu-id="24548-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="24548-176">Como você não instalou o MySQL, criaremos o diretório e montaremos o recurso DRBD.</span><span class="sxs-lookup"><span data-stu-id="24548-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span></span> <span data-ttu-id="24548-177">Para executar essa opção, execute o seguinte código `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="24548-177">To perform this option, run the following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="24548-178">Configurar MySQL</span><span class="sxs-lookup"><span data-stu-id="24548-178">Set up MySQL</span></span>
<span data-ttu-id="24548-179">Agora você está pronto para instalar o MySQL em `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="24548-179">Now you're ready to install MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="24548-180">Você tem duas opções para `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="24548-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="24548-181">Você pode instalar o mysql-server, que criará /var/lib/mysql e preenchê-lo com um novo diretório de dados, para então remover o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="24548-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span></span> <span data-ttu-id="24548-182">Para executar essa opção, execute o seguinte código `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="24548-182">To perform this option, run the following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="24548-183">A segunda opção é realizar failover para `hadb02` e, em seguida, instalar mysql-server lá.</span><span class="sxs-lookup"><span data-stu-id="24548-183">The second option is to failover to `hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="24548-184">Scripts de instalação perceberão a instalação existente e não tocarão nela.</span><span class="sxs-lookup"><span data-stu-id="24548-184">Installation scripts will notice the existing installation and won't touch it.</span></span>

<span data-ttu-id="24548-185">Execute o código a seguir no `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="24548-185">Run the following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="24548-186">Execute o código a seguir no `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="24548-186">Run the following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="24548-187">Se não pretende usar failover no DRBD agora, a primeira opção é mais fácil, embora indiscutivelmente menos elegante.</span><span class="sxs-lookup"><span data-stu-id="24548-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span></span> <span data-ttu-id="24548-188">Depois de configurá-lo, você pode começar a trabalhar no banco de dados do MySQL.</span><span class="sxs-lookup"><span data-stu-id="24548-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="24548-189">Execute o código a seguir em `hadb02` (ou qualquer um dos servidores ativos, de acordo com o DRBD):</span><span class="sxs-lookup"><span data-stu-id="24548-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* TO root;

> [!WARNING]
> <span data-ttu-id="24548-190">Esta última instrução desabilita efetivamente a autenticação para o usuário raiz nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="24548-190">This last statement effectively disables authentication for the root user in this table.</span></span> <span data-ttu-id="24548-191">Ela deve ser substituída pelas instruções GRANT de nível de produção e só é incluída para fins de ilustração.</span><span class="sxs-lookup"><span data-stu-id="24548-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="24548-192">Caso queira fazer consultas externas às VMs (que é a finalidade deste guia), você também precisará habilitar a rede para o MySQL.</span><span class="sxs-lookup"><span data-stu-id="24548-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span></span> <span data-ttu-id="24548-193">Em ambas as VMs, abra `/etc/mysql/my.cnf` e acesse `bind-address`.</span><span class="sxs-lookup"><span data-stu-id="24548-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span></span> <span data-ttu-id="24548-194">Altere o endereço de 127.0.0.1 para 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="24548-194">Change the address from 127.0.0.1 to 0.0.0.0.</span></span> <span data-ttu-id="24548-195">Depois de salvar o arquivo, emita uma `sudo service mysql restart` no primário atual.</span><span class="sxs-lookup"><span data-stu-id="24548-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-the-mysql-load-balanced-set"></a><span data-ttu-id="24548-196">Criar o conjunto de balanceamento de carga do MySQL</span><span class="sxs-lookup"><span data-stu-id="24548-196">Create the MySQL load-balanced set</span></span>
<span data-ttu-id="24548-197">Volte para o portal, acesse `hadb01` e escolha **Pontos de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="24548-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="24548-198">Para criar um ponto de extremidade, escolha MySQL (TCP 3306) na lista suspensa e selecione **Criar novo conjunto de balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="24548-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="24548-199">Nomeie o ponto de extremidade do balanceamento de carga como `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="24548-199">Name the load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="24548-200">Defina **Time** para 5 segundos no mínimo.</span><span class="sxs-lookup"><span data-stu-id="24548-200">Set **Time** to 5 seconds, minimum.</span></span>

<span data-ttu-id="24548-201">Depois de criar o ponto de extremidade, acesse `hadb02`, escolha **Pontos de Extremidade** e crie um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="24548-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="24548-202">Escolha `lb-mysql` e selecione MySQL na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="24548-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span></span> <span data-ttu-id="24548-203">Também é possível usar a CLI do Azure nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="24548-203">You can also use the Azure CLI for this step.</span></span>

<span data-ttu-id="24548-204">Agora você tem tudo o que precisa para uma operação manual do cluster.</span><span class="sxs-lookup"><span data-stu-id="24548-204">You now have everything you need for manual operation of the cluster.</span></span>

### <a name="test-the-load-balanced-set"></a><span data-ttu-id="24548-205">Testar o conjunto de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="24548-205">Test the load-balanced set</span></span>
<span data-ttu-id="24548-206">É possível executar testes de um computador externo usando qualquer cliente do MySQL ou por meio de determinados aplicativos, como phpMyAdmin em execução como um site do Azure.</span><span class="sxs-lookup"><span data-stu-id="24548-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="24548-207">Nesse caso, você usou a ferramenta de linha de comando do MySQL em outra caixa do Linux:</span><span class="sxs-lookup"><span data-stu-id="24548-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="24548-208">Executando failover manualmente</span><span class="sxs-lookup"><span data-stu-id="24548-208">Manually failing over</span></span>
<span data-ttu-id="24548-209">Você pode simular failovers desativando o MySQL, alternando o primário do DRBD e reiniciando o MySQL.</span><span class="sxs-lookup"><span data-stu-id="24548-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="24548-210">Para executar essa tarefa, execute o seguinte código em hadb01:</span><span class="sxs-lookup"><span data-stu-id="24548-210">To perform this task, run the following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="24548-211">Em seguida, em hadb02:</span><span class="sxs-lookup"><span data-stu-id="24548-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="24548-212">Depois de executar failover manualmente, você poderá repetir a consulta remota e ela deverá funcionar perfeitamente.</span><span class="sxs-lookup"><span data-stu-id="24548-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="24548-213">Configurar Corosync</span><span class="sxs-lookup"><span data-stu-id="24548-213">Set up Corosync</span></span>
<span data-ttu-id="24548-214">Corosync é a infraestrutura de cluster subjacente necessária ao funcionamento do Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="24548-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span></span> <span data-ttu-id="24548-215">Para Heartbeat (e outras metodologias como Ultramonkey), o Corosync é uma divisão das funcionalidades de CRM, enquanto o Pacemaker continua mais semelhante ao Heartbeat em funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="24548-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span></span>

<span data-ttu-id="24548-216">A restrição principal do Corosync no Azure é que o Corosync prefere comunicação multicast via broadcast via unicast, mas a rede do Microsoft Azure só é compatível com unicast.</span><span class="sxs-lookup"><span data-stu-id="24548-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="24548-217">Felizmente, o Corosync tem um modo unicast funcional.</span><span class="sxs-lookup"><span data-stu-id="24548-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="24548-218">A única restrição real é que, como todos os nós não estão se comunicando entre si, você precisa definir os nós em arquivos de configuração, inclusive seus endereços IP.</span><span class="sxs-lookup"><span data-stu-id="24548-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="24548-219">Podemos usar os arquivos de exemplo do Corosync para Unicast e alterar o endereço de associação, as listas de nós e os diretórios de registro em log (o Ubuntu usa `/var/log/corosync` e os arquivos de exemplo usam `/var/log/cluster`), além de habilitar as ferramentas de quorum.</span><span class="sxs-lookup"><span data-stu-id="24548-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="24548-220">Use a diretiva `transport: udpu` a seguir e os endereços IP definidos manualmente para ambos os nós.</span><span class="sxs-lookup"><span data-stu-id="24548-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="24548-221">Execute o código a seguir no `/etc/corosync/corosync.conf` em ambos os nós:</span><span class="sxs-lookup"><span data-stu-id="24548-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="24548-222">Copie esse arquivo de configuração em ambas as VMs e inicie o Corosync em ambos os nós:</span><span class="sxs-lookup"><span data-stu-id="24548-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="24548-223">Logo depois de iniciar o serviço, o cluster deverá estar estabelecido no anel atual e o quorum deverá estar constituído.</span><span class="sxs-lookup"><span data-stu-id="24548-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span></span> <span data-ttu-id="24548-224">Podemos verificar essa funcionalidade examinando logs ou executando o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="24548-224">We can check this functionality by reviewing logs or by running the following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="24548-225">Você verá saídas semelhantes à seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="24548-225">You will see output similar to the following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="24548-227">Configurando o Pacemaker</span><span class="sxs-lookup"><span data-stu-id="24548-227">Set up Pacemaker</span></span>
<span data-ttu-id="24548-228">O Pacemaker usa o cluster para monitorar recursos, definir quando os primários são desativados e mudar esses recursos para os secundários.</span><span class="sxs-lookup"><span data-stu-id="24548-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span></span> <span data-ttu-id="24548-229">Os recursos podem ser definidos com base em um conjunto de scripts disponíveis ou de scripts LSB (init-like), entre outras opções.</span><span class="sxs-lookup"><span data-stu-id="24548-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="24548-230">Queremos que o Pacemaker seja o “proprietário” do recurso DRBD, do ponto de montagem e do serviço MySQL.</span><span class="sxs-lookup"><span data-stu-id="24548-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span></span> <span data-ttu-id="24548-231">Se o Pacemaker puder ativar e desativar o DRBD, montar e desmontá-lo, e iniciar e parar o MySQL na ordem certa quando algo ruim acontecer com o primário, então a instalação estará concluída.</span><span class="sxs-lookup"><span data-stu-id="24548-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span></span>

<span data-ttu-id="24548-232">Ao instalar o Pacemaker pela primeira vez, a configuração deve ser bem simples, algo como:</span><span class="sxs-lookup"><span data-stu-id="24548-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="24548-233">Verifique a configuração executando `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="24548-233">Check the configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="24548-234">Crie, então, um arquivo (como `/tmp/cluster.conf`) com os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="24548-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="24548-235">Carregar o arquivo para a configuração.</span><span class="sxs-lookup"><span data-stu-id="24548-235">Load the file into the configuration.</span></span> <span data-ttu-id="24548-236">Você só precisa fazer isso em um nó.</span><span class="sxs-lookup"><span data-stu-id="24548-236">You only need to do this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="24548-237">Verifique se o Pacemaker é iniciado durante a inicialização em ambos os nós:</span><span class="sxs-lookup"><span data-stu-id="24548-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="24548-238">Usando `sudo crm_mon –L`, verifique se um dos nós se tornou o mestre do cluster e está executando todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="24548-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span></span> <span data-ttu-id="24548-239">Você pode usar montar e verificar se os recursos estão em execução.</span><span class="sxs-lookup"><span data-stu-id="24548-239">You can use mount and ps to check that the resources are running.</span></span>

<span data-ttu-id="24548-240">A captura de tela a seguir mostra `crm_mon` com um nó parado (saia selecionando Control+C):</span><span class="sxs-lookup"><span data-stu-id="24548-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="24548-242">Essa captura de tela mostra ambos os nós, um mestre e um subordinado:</span><span class="sxs-lookup"><span data-stu-id="24548-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="24548-244">Testando</span><span class="sxs-lookup"><span data-stu-id="24548-244">Testing</span></span>
<span data-ttu-id="24548-245">Você está pronto para uma simulação de failover automático.</span><span class="sxs-lookup"><span data-stu-id="24548-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="24548-246">Existem duas maneiras de fazer isso: a fácil e a difícil.</span><span class="sxs-lookup"><span data-stu-id="24548-246">There are two ways to do this: soft and hard.</span></span>

<span data-ttu-id="24548-247">A maneira fácil é usar a função de desligamento do cluster: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="24548-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="24548-248">Se você usar isso no mestre, o subordinado assumirá.</span><span class="sxs-lookup"><span data-stu-id="24548-248">If you use this on the master, the slave takes over.</span></span> <span data-ttu-id="24548-249">Lembre-se de defini-lo novamente como desativado.</span><span class="sxs-lookup"><span data-stu-id="24548-249">Remember to set this back to off.</span></span> <span data-ttu-id="24548-250">Caso contrário, o crm_mon mostrará um nó em espera.</span><span class="sxs-lookup"><span data-stu-id="24548-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="24548-251">A maneira mais difícil é desligar a VM primária (hadb01) por meio do portal ou alterar o nível de execução na VM (ou seja, parada e desligamento).</span><span class="sxs-lookup"><span data-stu-id="24548-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span></span> <span data-ttu-id="24548-252">Isso ajuda a Corosync e o Pacemaker, sinalizando que o mestre será desativado.</span><span class="sxs-lookup"><span data-stu-id="24548-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span></span> <span data-ttu-id="24548-253">Você pode testar isso (útil para janelas de manutenção), mas também é possível forçar o cenário apenas congelando a VM.</span><span class="sxs-lookup"><span data-stu-id="24548-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="24548-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="24548-254">STONITH</span></span>
<span data-ttu-id="24548-255">Deve ser possível emitir um desligamento da VM por meio da CLI do Azure, em vez de um script STONITH que controle um dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="24548-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="24548-256">É possível usar `/usr/lib/stonith/plugins/external/ssh` como base e habilitar STONITH na configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="24548-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span></span> <span data-ttu-id="24548-257">A CLI do Azure deve estar instalada globalmente e as configurações e perfil de publicação devem ser carregadas para o usuário do cluster.</span><span class="sxs-lookup"><span data-stu-id="24548-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span></span>

<span data-ttu-id="24548-258">Código de exemplo para o recurso está disponível no [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="24548-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="24548-259">Altere a configuração do cluster adicionando o seguinte a `sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="24548-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="24548-260">O script não realiza verificações de ligado/desligado.</span><span class="sxs-lookup"><span data-stu-id="24548-260">The script doesn't perform up/down checks.</span></span> <span data-ttu-id="24548-261">O recurso SSH original apresentava 15 verificações de ping, mas o tempo de recuperação de uma VM do Azure pode ser mais variável.</span><span class="sxs-lookup"><span data-stu-id="24548-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="24548-262">Limitações</span><span class="sxs-lookup"><span data-stu-id="24548-262">Limitations</span></span>
<span data-ttu-id="24548-263">As seguintes limitações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="24548-263">The following limitations apply:</span></span>

* <span data-ttu-id="24548-264">O script do recurso DRBD linbit que gerencia DRBD como um recurso no Pacemaker usa `drbdadm down` durante a desativação de um nó, mesmo que o nó esteja apenas em modo de espera.</span><span class="sxs-lookup"><span data-stu-id="24548-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span></span> <span data-ttu-id="24548-265">Isso não é o ideal, pois o subordinado não sincronizará o recurso DRBD enquanto o mestre receber gravações.</span><span class="sxs-lookup"><span data-stu-id="24548-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span></span> <span data-ttu-id="24548-266">Se o mestre não falhar normalmente, o escravo poderá assumir um estado do sistema de arquivos mais antigo.</span><span class="sxs-lookup"><span data-stu-id="24548-266">If the master does not fail graciously, the slave can take over an older file system state.</span></span> <span data-ttu-id="24548-267">Existem duas maneiras em potencial de resolver isso:</span><span class="sxs-lookup"><span data-stu-id="24548-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="24548-268">Impor um `drbdadm up r0` a todos os nós de cluster por meio de um watchdog local (não clusterizado)</span><span class="sxs-lookup"><span data-stu-id="24548-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="24548-269">Editando o script DRBD linbit, verificando se `down` não é chamado em `/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="24548-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="24548-270">O balanceador de carga precisa de pelo menos cinco segundos para responder, por isso os aplicativos devem reconhecer o cluster e ser mais tolerantes quanto ao tempo limite.</span><span class="sxs-lookup"><span data-stu-id="24548-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="24548-271">Outras arquiteturas, como filas no aplicativo e middleware de consulta também podem ajudar.</span><span class="sxs-lookup"><span data-stu-id="24548-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="24548-272">O ajuste do MySQL é necessário para garantir que a gravação ocorra em um ritmo gerenciável e que os caches sejam liberados para o disco com a maior frequência possível a fim de minimizar a perda de memória.</span><span class="sxs-lookup"><span data-stu-id="24548-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span></span>
* <span data-ttu-id="24548-273">O desempenho da gravação dependerá da interconexão da VM no comutador virtual, pois esse é o mecanismo usado pelo DRBD para replicar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24548-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span></span>
